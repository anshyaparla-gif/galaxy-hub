import random
from Bio.Seq import Seq

# Define start and stop codons
start_codon = "ATG"
stop_codons = ['TAA', 'TAG', 'TGA']
while True:
    max_attempts = 20
    attempts = 0
    success = False


    # Loop to handle user input validation
    while attempts < max_attempts:
        # 1. Ask for input inside the loop so it can repeat
        user_dna_body = input("Please enter the DNA body (A, T, C, G): ").upper()
    
        # 2. Check if characters are valid
        if not all(base in 'ATGC' for base in user_dna_body):
            print("Invalid DNA sequence. Only 'A', 'T', 'G', 'C' are allowed.")
            attempts += 1
            print(f"Attempts remaining: {max_attempts - attempts}\n")
            continue  # Skip to the next iteration to ask again
            
        # 3. Check if the length is a multiple of 3
        if len(user_dna_body) % 3 != 0:
            print("This sequence does not have a multiple of three number of bases.")
            attempts += 1
            print(f"Attempts remaining: {max_attempts - attempts}\n")
            continue  # Skip to the next iteration to ask again
        
        # If both conditions pass, break out of the loop
        success = True
        break
    if not success:
        print("\nMaximum attempts reached.")
        break

    # Process results if the user provided valid input within 20 attempts
    if success:
        # Assemble the full coding sequence after successful input
        a_simple_sequence = Seq(start_codon + user_dna_body + random.choice(stop_codons))
    
        print(f"\nGenerated DNA Sequence: {a_simple_sequence}")

        sequence_str = str(a_simple_sequence) 
        gc_count = sequence_str.count('G') + sequence_str.count('C')
        total_bases = len(sequence_str)
    
        if total_bases > 0:
            gc_percentage = (gc_count / total_bases) * 100
            print(f"The GC content is {round(gc_percentage, 0)}%")
        else:
            print("Cannot calculate GC content for an empty sequence.")

        adenosine_count = a_simple_sequence.count("A")
        thymine_count = a_simple_sequence.count("T")
        cytosine_count = a_simple_sequence.count("C")
        guanine_count = a_simple_sequence.count("G")

        print(f"There are {adenosine_count} adenines, {thymine_count} thymines, {cytosine_count} cytosines, and {guanine_count} guanines.")
        print(f"Total nucleotides: {total_bases}")

        com = a_simple_sequence.complement()
        revcom = a_simple_sequence.reverse_complement()
        transcom = a_simple_sequence.transcribe()
        translcom = a_simple_sequence.translate()

        print(f"Complement: {com}")
        print(f"Reverse Complement: {revcom}")
        print(f"Transcript (RNA): {transcom}")
        print(f"Translation (Amino Acids): {translcom}")
        user_other_dna_body = input("That was fun! Type S to try another DNA sequence: ").upper()

    if user_other_dna_body != "S":
        break




















