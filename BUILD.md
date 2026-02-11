# Building AILS2

## Prerequisites

1. **Install Java JDK** (version 8 or higher):
   ```bash
   # On Ubuntu/WSL:
   sudo apt update
   sudo apt install openjdk-17-jdk
   
   # Verify installation:
   java -version
   javac -version
   ```

## Building the JAR

AILS2 is a Java project. To build it:

### Option 1: Manual Compilation (if source files are present)

If the repository contains Java source files in a `src/` directory:

```bash
cd solver/ails2

# Find all Java files
find src -name "*.java" > sources.txt

# Compile all Java files
javac -d build/classes @sources.txt

# Create JAR file with manifest
mkdir -p build/classes/META-INF
echo "Main-Class: SearchMethod.AILSII" > build/classes/META-INF/MANIFEST.MF

# Create JAR
jar cfm AILSII.jar build/classes/META-INF/MANIFEST.MF -C build/classes .

# Or simpler (if main class is known):
jar cfe AILSII.jar SearchMethod.AILSII -C build/classes .
```

### Option 2: Check if JAR already exists

The JAR file might already be built. Check:
```bash
cd solver/ails2
find . -name "*.jar" -o -name "AILSII.jar"
```

### Option 3: Download Pre-built JAR

Check the original repository for a releases section or pre-built JAR:
- https://github.com/vinymax10/AILS-CVRP
- https://github.com/INFORMSJoC/2023.0106 (official INFORMS repository)

## Testing the Build

Once you have `AILSII.jar`, test it:

```bash
cd solver/ails2
java -jar AILSII.jar -file data/X-n110-k13.vrp -rounded true -best 0 -limit 10 -stoppingCriterion Time
```

## Troubleshooting

- **"java: command not found"**: Install Java JDK (see Prerequisites)
- **"javac: command not found"**: Install Java JDK (not just JRE)
- **"Could not find or load main class"**: Check the main class name in the source code
- **"No Java files found"**: The source might be in a different location or the submodule needs to be updated

## Note

If the repository structure is different, you may need to:
1. Check the original repository README
2. Look for build scripts (build.sh, compile.sh, etc.)
3. Check for Maven/Gradle configuration files
4. Contact the repository maintainers
