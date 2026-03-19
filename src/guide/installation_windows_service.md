# Windows Service (manual installation)

A standalone ZIP package is also provided:

```
midi-router-client-cli-<version>-win64.zip
```

This package contains:

- A **standard Windows service executable**  
- A **CLI executable** (same binary) for Linux/macOS‑style command‑line usage

Because this ZIP is **not installed via winget**, Windows users must **manually upgrade the service** for each new version:

1. Download the new ZIP  
2. Extract it  
3. Test the executable (important for unsigned binaries)  
4. Update the Windows service to point to the new version

Below are the correct commands.

---

## Updating the Windows Service Manually

Replace `<path>` with the full path to the extracted folder.

### 1. Test the executable (important for unsigned binaries)

Before registering it as a service, ensure Windows allows the executable to run:

```cmd
midi-router-client-cli.exe --headless
```

If Windows prompts for authorization, approve it.  
Once it runs successfully, continue with the service update.

---

### 2. Stop the existing service

```cmd
sc stop MidiRouterCli
```

### 3. Delete the existing service

```cmd
sc delete MidiRouterCli
```

### 4. Re‑create the service with the new version

⚠️ **Important:**  
`binPath=` must be followed by a space before the quoted path, or Windows will reject the command.

```cmd
sc create MidiRouterCli binPath= "D:\midi-router-client-cli-2.21.0-win64\bin\midi-router-client-cli.exe"
```

### 5. Start the service

```cmd
sc start MidiRouterCli
```

---

## Notes

- The service name is **MidiRouterCli**  
- The executable must remain in the same location after creation  
- If you move or delete the folder, the service will fail to start  
- Upgrading requires repeating the stop/delete/create/start sequence  
- Running the executable once manually ensures Windows trusts the unsigned binary before it runs as a service

