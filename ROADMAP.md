# ROADMAP.md — tensorflowOpencv

## 12-Month Vision

Transform the tensorflowOpencv project from a legacy single-platform TensorFlow/OpenCV demo into a production-grade, hardware-adaptive inference framework supporting four heterogeneous platforms with automated CI/CD, comprehensive testing, and real-time benchmarking.

---

## Quarterly Milestones

### Q1: Foundation (Months 1–3)

**Goal**: Establish modern build system, remove legacy dependencies, enable cross-platform compilation.

| Milestone | Status | Deliverables |
|---|---|---|
| CMake 4.0 build system | ✅ Planned | CMakeLists.txt with C++26 support, Ninja generator, conda py314 env |
| OpenCV v5 migration | ✅ Planned | Replace deprecated `dnn::Importer` with `cv::dnn::readNetFromTensorFlow`; remove `dnn::Blob` API |
| Remove hardcoded paths | ✅ Planned | Configurable model/image paths via CLI args and TOML config |
| Windows 11 + Ubuntu 26.04 builds | ✅ Planned | CI pipeline with GitHub Actions for both platforms |
| Basic test suite | ✅ Planned | pytest tests: model loading, inference correctness, output validation |
| README.md | ✅ Planned | Setup instructions, usage examples, architecture overview |

### Q2: Hardware Optimization (Months 4–6)

**Goal**: Enable hardware-specific inference backends and achieve measurable performance gains.

| Milestone | Status | Deliverables |
|---|---|---|
| NVIDIA Spark CUDA 13 backend | ✅ Planned | Tensor Core kernel fusion, CUDA graph capture for batch inference |
| Apple M5 Max CoreML dispatch | ✅ Planned | Neural Engine direct inference via CoreML integration |
| Intel Ultra 9 AVX-512 kernels | ✅ Planned | Optimized DNN forward pass with AVX-512 SIMD intrinsics |
| Raspberry Pi 5 ARM64 support | ✅ Planned | NEON-optimized inference, lightweight binary, cross-compilation |
| Performance benchmarking suite | ✅ Planned | Automated profiling: latency, throughput, memory per platform |
| Docker images per platform | ✅ Planned | Containerized builds with CUDA, OpenCV v5, Python 3.14 |

### Q3: Advanced Features (Months 7–9)

**Goal**: Add multi-model inference, streaming support, and ONNX Runtime integration.

| Milestone | Status | Deliverables |
|---|---|---|
| ONNX Runtime backend | ✅ Planned | Dual TF/ONNX inference with automatic backend selection |
| Batch processing pipeline | ✅ Planned | Thread-safe model pool, concurrent multi-stream inference |
| Real-time video inference | ✅ Planned | OpenCV VideoCapture integration with live classification overlay |
| Model format conversion tools | ✅ Planned | CLI tools for TF→ONNX, ONNX→OpenVINO conversion |
| Memory optimization | ✅ Planned | Model quantization (INT8), memory-mapped model loading |
| Integration tests | ✅ Planned | End-to-end tests: video stream → inference → output |

### Q4: Production Readiness (Months 10–12)

**Goal**: Hardened release, documentation, community infrastructure.

| Milestone | Status | Deliverables |
|---|---|---|
| v1.0 release | ✅ Planned | Tagged release with changelog, binary artifacts |
| Comprehensive documentation | ✅ Planned | Architecture docs, API reference, optimization guides |
| CI/CD full pipeline | ✅ Planned | Automated build → test → benchmark → release |
| OpenVINO integration | ✅ Planned | Third inference backend for Intel hardware |
| Monitoring & telemetry | ✅ Planned | Inference metrics collection, JSON export |
| Community contributions | ✅ Planned | Contributing guide, issue templates, code of conduct |

---

## Technical Debt

| Item | Priority | Description | Estimated Effort |
|---|---|---|---|
| Remove hardcoded Windows paths | 🔴 High | `Tensorflow13OpenCV33VS2015.cpp:47-48` contains hardcoded `C:/opencv33/FarshidPirahanSiah/` paths | 1 day |
| Remove deprecated `dnn::Blob` API | 🔴 High | `tfOpenCVtest.cpp` uses removed `dnn::Blob::fromImages` — must migrate to `blobFromImage` | 2 days |
| Remove `dnn::Importer` usage | 🔴 High | Both files use deprecated `createTensorflowImporter` — replace with `readNetFromTensorFlow` | 1 day |
| Add CMakeLists.txt | 🔴 High | No build system exists — project only builds via VS2015 .sln (not in repo) | 2 days |
| Add README.md | 🟡 Medium | No documentation exists for setup, usage, or architecture | 1 day |
| Remove `using namespace std` | 🟡 Medium | Pollutes global namespace — use explicit `std::` prefixes | 0.5 days |
| Remove debug UI calls | 🟡 Medium | `imshow`/`cvWaitKey`/`cin >> farshid` are debugging artifacts | 0.5 days |
| Add proper error handling | 🟡 Medium | Multiple `exit(-1)` calls — replace with exceptions or error codes | 2 days |
| Add unit tests | 🟡 Medium | Zero test coverage — need model loading, inference, and output validation tests | 3 days |
| Fix `dnn::initModule()` removal | 🟢 Low | `tfOpenCVtest.cpp:42` calls removed function — remove or replace | 0.5 days |
| Remove OpenCL toggle hack | 🟢 Low | `ocl::setUseOpenCL(false)` should be configurable, not hardcoded | 0.5 days |
| Add `.gitignore` | 🟢 Low | No gitignore — binary files, build artifacts may be committed accidentally | 0.5 days |

---

## Future Features

### Short-Term (3–6 months)

- **Multi-model ensemble inference**: Run multiple models (Inception, ResNet, EfficientNet) simultaneously with weighted voting
- **Video stream classification**: Real-time classification on live camera feeds with FPS overlay
- **Model quantization CLI**: INT8/FP16 quantization tool for edge deployment on Raspberry Pi
- **Configurable preprocessing**: Support different normalization strategies per model (mean subtraction, scaling, channel ordering)

### Medium-Term (6–12 months)

- **ONNX Runtime backend**: Load and run ONNX models alongside TensorFlow FrozenGraph
- **OpenVINO integration**: Intel-optimized inference for Ultra 9 and discrete GPUs
- **REST API server**: Expose inference via HTTP/JSON for microservice deployment
- **Batch video processing**: Process video files frame-by-frame with output CSV/JSON

### Long-Term (12+ months)

- **Distributed inference**: Multi-GPU inference across NVIDIA Spark partitions
- **Edge deployment pipeline**: Automated optimization and packaging for Raspberry Pi 5 deployment
- **Custom model training integration**: Fine-tune Inception on custom datasets with OpenCV-based data augmentation
- **WebAssembly frontend**: Browser-based inference demo using OpenCV.js and ONNX Runtime Web
