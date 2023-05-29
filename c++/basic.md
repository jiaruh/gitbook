# basic

* read from files

```cpp
void decodeBase64File(const std::string& file_path) {
    // Read the base64 encoded file
    std::ifstream encoded_file(file_path);
    if (!encoded_file) {
        std::cerr << "Failed to open file: " << file_path << std::endl;
        return;
    }

    std::stringstream buffer;
    buffer << encoded_file.rdbuf();
    std::string encoded_string = buffer.str();

    // Decode the base64 content
    std::string decoded_string = base64_decode(encoded_string);

    // Determine the output file path
    std::string output_file_path = file_path;
    size_t file_extension_pos = output_file_path.rfind(".");
    output_file_path = output_file_path.substr(0, file_extension_pos) + "_decoded" +
                       output_file_path.substr(file_extension_pos);

    // Write the plain text to the output file
    std::ofstream output_file(output_file_path);
    if (!output_file) {
        std::cerr << "Failed to create output file: " << output_file_path << std::endl;
        return;
    }
    output_file << decoded_string;

    std::cout << "Decoded content saved to: " << output_file_path << std::endl;
}
```
