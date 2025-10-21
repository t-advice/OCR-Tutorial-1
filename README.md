# OCR Vision Tutorial (._NET MAUI, .NET 9_)

A minimal .NET MAUI tutorial app that captures an image and extracts its text using OCR (Optical Character Recognition). The goal is to get an OCR-powered vision flow up and running end-to-end: take a photo or pick one, run OCR, and display the recognized text in the UI.

## Features
- Capture a photo or pick an image from the gallery.
- Run OCR on-device or via a cloud vision service.
- Display extracted text with simple copy/share options.
- Cross-platform: Android, iOS, Windows, macOS (Mac Catalyst).

## Prerequisites
- Visual Studio 2022 (latest) with the __.NET Multi-platform App UI development__ workload.
- .NET 9 SDK installed.
- Platform tooling:
  - Android: Android SDK and an emulator or device.
  - iOS/Mac: Xcode + __Tools > iOS > Pair to Mac__ (on Windows) if targeting iOS.
  - Windows: Windows 10/11 with WinUI dependencies (installed by the MAUI workload).

Install workloads (if needed):

## Getting Started
1. Clone the repository and open the solution in Visual Studio 2022.
2. Restore dependencies:
   - From VS: __Build > Restore NuGet Packages__
   - Or CLI: `dotnet restore`
3. Select the startup project (the .NET MAUI app).
4. Choose a target from the debug dropdown (Android, iOS, Windows, Mac Catalyst).
5. Run:
   - Press __F5__ (Debug) or __Debug > Start Debugging__
   - Or use __Ctrl+F5__ (Run without debugging)

CLI (optional):

## Configuring OCR
This tutorial supports two typical approaches. Pick one:

- Local (device) OCR:
  - Integrate a MAUI-compatible OCR library (e.g., a Tesseract binding).
  - Bundle or deploy trained language data as required by the library.
  - Pros: works offline. Cons: larger app size, device-dependent accuracy.

- Cloud OCR (e.g., Azure AI Vision “Read”):
  - Create a Vision resource, note the Endpoint and Key.
  - Set configuration values securely (do not hardcode secrets):
    - Preferred: platform secrets or secure storage per OS.
    - During development, environment variables (e.g., `VISION_ENDPOINT`, `VISION_KEY`) can be used.
  - Pros: high accuracy and language support. Cons: requires network and incurs costs.

The app’s OCR service abstraction allows you to swap implementations with minimal UI changes.

## Permissions
- Android:
  - Camera: `android.permission.CAMERA`
  - Gallery/Photos (API 33+): `android.permission.READ_MEDIA_IMAGES`
- iOS/macOS:
  - Add `NSCameraUsageDescription` and `NSPhotoLibraryAddUsageDescription` to `Info.plist`.

Ensure these are configured in platform projects before running on devices.

## How It Works
- Image acquisition: camera capture or gallery pick.
- OCR processing: the selected OCR backend converts the image to text.
- Result rendering: recognized text is shown in the UI with basic actions.

## Project Structure (high level)
- UI (Pages/Views): capture/pick, show result
- Services:
  - `IImagePickerService` (camera/gallery)
  - `IOcrService` (local or cloud implementation)
- Platforms: platform-specific permissions and setup

## Troubleshooting
- Emulator/device not detected: check __Device Manager__ (Android) and ensure platform tooling is installed.
- Permission errors: verify platform-specific manifests/capabilities.
- Workload issues: run `dotnet workload restore` and restart Visual Studio.
- iOS build on Windows: pair to a Mac via __Tools > iOS > Pair to Mac__.

## Roadmap (Optional)
- Multi-language OCR
- Text regions and confidence overlays
- Save/export recognized text
- Batch processing

## Security
- Never commit API keys. Use secure storage or developer secrets.
- If using cloud OCR, monitor usage and costs.

## License
Specify your license here.