# Assignment 4 - CIDR Block Validator
In this assignment you will create a program that will take a CIDR block as input and validate a series of IP addresses to determine if they fall within the block range.

The program will be written in C.

## Input
The program will take the CIDR block as input and will then prompt the user to input IP addresses one at a time.  The program should exit if the CIDR block does not start on an appropriate boundary.  The program will terminate when the user indicates they are finished by entering 'q'.

## Output
Your program should produce the following interaction.  Note lines beginning with the word "Enter" contain text entered by the user (after the colon).

	Enter a CIDR block range (CIDR notation): 192.168.0.0/16
	IP Range: 192.168.0.0 (0xc0a80000) to 192.168.255.255 (0xc0a8ffff)
	Mask: 255.255.0.0 (0xffff0000)

	Enter an address (q to quit): 192.169.0.5
	192.169.0.5 is out of range

	Enter an address (q to quit): 192.168.0.5
	192.168.0.5 is within range

	Enter an address (q to quit): q

## Implementation Notes
Your program should prompt the user for a CIDR block that will be provided in CIDR notation (example: 192.168.0.0/16).  After validating the CIDR block (by determining if the host bits are all zeros) it will then use this input to compute the subnet mask (to be used later in determining if each address is within the block).  Once the subnet mask has been computed, the program will begin prompting the user for IP addresses to be validated against the CIDR block.  The program will continue prompting the user for another IP address until the user enters 'q' to quit.

### Functions
Your program must provide implementations for the following functions:

 - `uint32_t bit_count_to_mask(int)`
   - This function returns the subnet mask as a 32 bit field based on the integer provided.  The integer indicates the desired number of network bits to be set in the mask.
   - **Note**: The integer is assumed to be derived from the CIDR block expression (the number after the '/')
   - **Returns**:  an `uint32_t` field containing the 4 octets representing the subnet mask
   - **Parameters**:
      1. the integer representing the number of network bits in the subnet mask.

 - `uint32_t ipv4_to_uint32(char *)`
   - This function returns an IP address as a 32 bit field based on the string provided.  The string is the IP address.
   - **Note**: The IP Address is assumed to be derived from the CIDR block expression (the number before the '/')
   - **Returns**:  an `uint32_t` field containing the 4 octets representing the IP address
   - **Parameters**:
      1. the address of the character array containing the IP address as a string.

 - `void uint32_to_ipv4(uint32_t, char *)`
   - This function stores a string representation of a 32 bit IP address field, into the array provided.  In other words, it converts a 32 bit field into a string that is formatted as an IP address.
   - **Returns**:  Nothing
   - **Parameters**:
      1. the field containing an IP address represented as a 32 bit integer.
      2. the address of the character array that will hold the string representation of the IP address

### Input Valiation
In the event that the CIDR block provided does not pass the validation, the error message below must be provided:

	Enter a CIDR block range (CIDR notation): 192.168.5.0/16
	Error: starting address should be on a correct boundary

Note that the validation logic consists of confirming that the host bits of the starting IP address (the value before the '/') should all be set to 0.  The boundary between host and network bits is determined by the subnet mask that is derived from the integer after the '/'.
