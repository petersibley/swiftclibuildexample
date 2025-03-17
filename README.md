# Simple Swift CLI with XcodeGen

This project demonstrates how to use **XcodeGen** to create a Swift command-line tool on macOS **without needing the full Xcode editor**.

By using **XcodeGen**, we can generate an Xcode project from a simple JSON specification, compile it using `xcodebuild`, and run the command-line app—all from the terminal.

---

## 1️⃣ Install Dependencies

Ensure you have **Homebrew** installed. If not, install it with:
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then install the required tools:
```sh
brew install xcodegen xcbeautify
```

---

## 2️⃣ Create the Swift Source File

Create a simple Swift file named `main.swift`:
```sh
vi main.swift
```

Add the following content:
```swift
print("Hello, World!")
```

Save and exit (`ESC` → `:wq` in Vim).

---

## 3️⃣ Define the Xcode Project Configuration

Create `project.json`:
```sh
vi project.json
```

Add the following JSON configuration:
```json
{
  "name": "simpletest",
  "targets": {
    "simpletest": {
      "platform": "macOS",
      "deploymentTarget": "15.2",
      "sources": ["main.swift"]
    }
  }
}
```

---

## 4️⃣ Generate the Xcode Project

Run the following command to generate the `.xcodeproj` file:
```sh
xcodegen generate --spec project.json
```

This will create `simpletest.xcodeproj`, which is required to build the project.

---

## 5️⃣ Compile the Project

To compile the project, run:
```sh
xcodebuild -project simpletest.xcodeproj -scheme simpletest -configuration Debug -derivedDataPath ./build | xcbeautify
```

This will compile the project and store the output in `./build/`.

---

## 6️⃣ Run the Command-Line App

Once the build succeeds, run the binary:
```sh
./build/Build/Products/Debug/simpletest
```

Expected output:
```
Hello, World!
```

---

## ✅ Summary of Steps

1. **Install dependencies** → `brew install xcodegen xcbeautify`
2. **Create `main.swift`** → Add a simple print statement
3. **Create `project.json`** → Define the Xcode project settings
4. **Generate the Xcode project** → `xcodegen generate --spec project.json`
5. **Compile the project** → `xcodebuild ... | xcbeautify`
6. **Run the CLI app** → `./build/Build/Products/Debug/simpletest`

---

This **README** provides a complete and structured guide to setting up and running a **Swift command-line tool** using **XcodeGen**. 🚀

