# Windows Service 

In most situations, you don’t need to install it as a service.

## **MidiRouterClient CLI / Windows Service**  

run as administrator 

```
scoop install -g midi-router-client-cli
```

keep updated with

```
# as admin, this will also update all user scoop apps
scoop update -g --all
```

After installation, it is possible to start the service from an elevated shell:

```
sc start MidiRouterClientCli
```

---

### ⚠️ MidiRouterClient Windows Service Configuration Files

Windows services **do not** use the same AppData folder as your logged‑in user.  
This means the GUI/CLI app and the background service each store their configuration in **different locations**.

It is possible to change the service’s Run As account at windows service manager to your own user to avoid this issue entirely.

Additionally, if the service version does not match the GUI version, 
configuration corruption and data loss may occur.

The service’s startup sequence may also depend on the internal `midisrv` component.
Adding `midisrv` as a service dependency can be helpful, especially when modern MIDI 2.0 virtual ports are defined.

#### 🧍 Normal application (GUI or CLI run manually)

Your user‑level configuration is stored here:

```
C:\Users\<YourUser>\AppData\Roaming\shemeshg\MidiRouterClient.ini
```

#### 🖥️ Windows service (running as LocalSystem)

The service runs under the **system account**, which has its own profile.  
Its configuration file is stored here:

```
C:\Windows\System32\config\systemprofile\AppData\Roaming\shemeshg\MidiRouterClient.ini
C:\Windows\System32\config\systemprofile\AppData\Local\midiRouterClient.json
```

This is the file the **service** reads — for example, to determine which port to listen on.

#### 📌 Why this matters

- Editing the **user** INI file does *not* affect the service  
- Editing the **service** INI file does *not* affect your user app  
- If you want the service to use the same settings as your user app, you must manually copy or edit the service’s INI file in the `systemprofile` directory

