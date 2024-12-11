Below is a final `README.md` that consolidates all the requested information and clearly explains the project's purpose, setup, and usage:

```markdown
# Whisper C++ + TensorRT Integration

**Author:** Manu Bhardwaj ([@ifitsmanu](https://github.com/ifitsmanu))

This project integrates [OpenAI's Whisper](https://github.com/openai/whisper) for automatic speech recognition into a pure C++ environment with **NVIDIA TensorRT** for optimized inference. It includes a pipeline for audio preprocessing, tokenization, and Voice Activity Detection (VAD) - all without relying on ONNX for VAD models.

## Key Features

- **TensorRT Accelerated Whisper**:  
  Leverages pre-converted TensorRT engine (`.plan`) files for the Whisper encoder and decoder, providing improved inference speed and reduced memory usage on NVIDIA GPUs.

- **No ONNX Dependency for VAD**:  
  Integrates a custom or TRT-based VAD solution directly in C++, avoiding ONNXRuntime dependency. This allows a seamless end-to-end pipeline entirely within the TensorRT ecosystem or your chosen VAD method.

- **Audio Preprocessing**:  
  Includes audio normalization, mel-spectrogram extraction, and integration with FFT libraries (e.g., `kissfft`) for efficient signal processing.

- **Tokenizer (Optional)**:  
  A built-in tokenizer can be used for converting between tokens and text. Adjust as needed or rely on Whisper’s own tokenization logic if supported directly.


## Getting Started

### Dependencies

- **TensorRT** (8.x+): Ensure TensorRT is installed and accessible.  
- **C++17 or later**: Utilize modern C++ features.  
- **KissFFT** (Optional): For FFT-based audio preprocessing.  
- **CUDA Toolkit**: Required for GPU acceleration with TensorRT.

### Building the Project

1. Clone the repository:
   ```bash
   git clone https://github.com/ifitsmanu/whisper_trt.git
   cd whisper_trt
   ```

2. Create a build directory and run CMake:
   ```bash
   mkdir build && cd build
   cmake ..
   make
   ```

This will produce an executable (for example, `whisper_trt_exe`).

### Running Inference

Run the executable and provide arguments as needed (implement argument parsing in `main.cpp`):

```bash
./my_whisper_trt_exe --audio ../data/audio_samples/sample.wav
```

This command should:

- Preprocess the audio (convert to mel-spectrogram).
- Run VAD to determine where speech is present.
- Pass the relevant audio frames through the Whisper encoder/decoder via TensorRT.
- Convert the resulting tokens back into text and print/output the transcript.

## Testing

Tests are located in the `tests/` directory. After building:

```bash
cd build
ctest
```

This runs the test suite, which may include unit and integration tests for audio, model, tokenizer, VAD, and utilities.

## Notes & Further Development

- Integrate CUDA kernels or custom ops in `model.cpp` if needed.
- Fine-tune tokenizer logic in `tokenizer.cpp` or rely on Whisper’s built-in tokenization if available.
- Experiment with different FFT libraries or GPU-accelerated audio preprocessing.

## License

Refer to `LICENSE.md` for licensing details.

---

**Author:** Manu Bhardwaj ([@ifitsmanu](https://github.com/ifitsmanu))  
If you have suggestions or encounter issues, feel free to open an issue or submit a PR.