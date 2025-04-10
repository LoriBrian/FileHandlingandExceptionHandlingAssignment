# FileHandlingandExceptionHandlingAssignment

def modify_and_write_file(input_filename, output_filename):
    """
    Reads each line from an input file, modifies it, and writes the modified
    version to a new output file.

    Args:
        input_filename (str): The name of the file to read from.
        output_filename (str): The name of the file to write to.
    """
    try:
        with open(input_filename, 'r') as infile, open(output_filename, 'w') as outfile:
            for line in infile:
                # Simple modification: Add a line number to each line
                modified_line = f"Modified: {line.strip()}\n"
                outfile.write(modified_line)
        print(f"Successfully read from '{input_filename}' and wrote to '{output_filename}'.")
    except FileNotFoundError:
        print(f"Error: Input file '{input_filename}' not found.")
    except IOError:
        print(f"Error: Could not read from or write to the files.")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

def get_and_read_user_file():
    """
    Asks the user for a filename and attempts to read and print its content,
    handling potential FileNotFoundError and IOError.
    """
    while True:
        filename = input("Enter the filename you want to read: ")
        try:
            with open(filename, 'r') as file:
                print(f"\nContents of '{filename}':")
                for line in file:
                    print(line, end='')  # Keep the original newline
            print("\nFile reading successful.")
            break  # Exit the loop if reading is successful
        except FileNotFoundError:
            print(f"Error: File '{filename}' not found. Please enter a valid filename.")
        except IOError:
            print(f"Error: Could not read file '{filename}'. Please check file permissions.")
        except Exception as e:
            print(f"An unexpected error occurred: {e}. Please try again.")

if __name__ == "__main__":
    print("--- File Read & Write Challenge ---")
    input_file = "input.txt"  # You can change this filename
    output_file = "output_modified.txt"

    # Create a sample input file for testing
    try:
        with open(input_file, 'w') as f:
            f.write("This is the first line.\n")
            f.write("Another line of text.\n")
            f.write("The final line in the input file.\n")
        print(f"Sample input file '{input_file}' created.")
    except IOError:
        print(f"Error: Could not create the sample input file '{input_file}'.")

    modify_and_write_file(input_file, output_file)
    print("\n--- Error Handling Lab ---")
    get_and_read_user_file()
