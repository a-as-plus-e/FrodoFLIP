# FrodoFLIP
Frodo FLIPS -- Key Recovery Attack

All project directories are stored as zip files.

# Ciphertexts

- This directory contains our database of Mu files that can be used to generate ciphertext artifacts. Using the public key, and modifying the encapsulate function to take mu as a parameter, the Sp and ct files may be generated. Code for this will be supplied shortly. In the meantime, the pre-created files are temporarily hosted at the following shared link(https://uark.box.com/s/ozjc0bdx4bamaady4zbhiqzkep7a1bcv). Sp files contain the S', E', and E'' matrices that generated the ciphertexts, Mu files contain the specific message randomness that generated S', E', and E''. ct files contain the output ciphertexts. To use the full database in secret key recovery, merge all files with the same name into one with a clever cat command.

# Key

- This contains the generated poisoned public key and related information.

# DFR Scripts

- This directory contains all of the scripts for generating DFR estimates under different rowhammer bit patterns and filter criteria. The main script to run is in the jupyter notebook, dfr_estimates.ipynb

# FrodoKEM Rowhammer

- This directory contains all code necessary to profile a machine and execute the end-to-end rowhammer attack, including performance degradation. The output of this step is the key directory used in subsequent steps.

# Supercomputer

- This directory contains all code necessary to generate the ciphertext DB on a supercomputer.

# Secret Key Recovery

- In the secret key recovery directory, there are two sageMath scripts, recover_key_column.sage and process_exp_key.sage, as well as a modified FrodoKEM python implementation.

- recover_key_column.sage takes the ciphertext DB generated in the super computing step, and attempts to recover the specified column. Repeat the use of the script for each column you want to recover. Combine the outputs to pass to the next script.

- process_exp_key.sage takes the experimentally recovered columns and generates a secret key that can be used as input to FrodoKEM.Decaps

# Session Key Recovery

- The session key recovery directory contains the c program used to test the session key bruteforce. A modified FrodoKEM C implementation is supplied to assist. In addition, the experimental key from the Secret Key Recovery step is added to the key directory. Thus, first compile FrodoKEM, then compile the bruteforce script as
    - gcc -o frodo-session-key-bruteforce.c frodo-session-key-bruteforce.c -lm -lfrodo -lcrypto -L .

- Run the program by supplying the missing column index (2, in our case).

- The program will output the session key if it is possible to recover.
