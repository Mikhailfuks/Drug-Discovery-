using Chem.NET;
using System;
using System.Collections.Generic;
using System.Linq;

public class DrugDiscoveryExample
{
    public static void Main(string[] args)
    {
        // Example molecules
        Molecule targetMolecule = new Molecule("C1=CC=CC=C1"); // Benzene
        Molecule candidateMolecule1 = new Molecule("CC(C)C"); // Isopentane
        Molecule candidateMolecule2 = new Molecule("c1ccccc1"); // Benzene

        // Calculate Tanimoto similarity scores (example descriptor)
        double similarity1 = targetMolecule.CalculateTanimotoSimilarity(candidateMolecule1);
        double similarity2 = targetMolecule.CalculateTanimotoSimilarity(candidateMolecule2);

        Console.WriteLine($"Similarity between target and candidate 1: {similarity1}");
        Console.WriteLine($"Similarity between target and candidate 2: {similarity2}");

        // Simple virtual screening (select molecules above a similarity threshold)
        double threshold = 0.8;
        List<Molecule> similarCandidates = new List<Molecule> { candidateMolecule1, candidateMolecule2 }
            .Where(m => targetMolecule.CalculateTanimotoSimilarity(m) > threshold)
            .ToList();

        Console.WriteLine($"Similar candidates: {string.Join(", ", similarCandidates.Select(m => m.SmilesString))}");
    }
}
