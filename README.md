# Native Windows audio bindings for Node.js
Nodejs bindings for Windows audio management 

## Installation 
```
npm install native-audio-bindings-win
```

## Usage
```javascript
import AudioNativeWin from 'native-audio-bindings-win';

const sessions = AudioNativeWin.getAllSessions();

// Printout the volume of each process
sessions.forEach((session) => {
  console.log(`${session.name ?? 'master'}: ${session.getVolume() * 100}%`)
});

// Set the volume of a single process
sessions
  .filter((session) => session.name === "process.exe")
  .forEach((session) => {
    session.setVolume(0.1); // 10%
  });

// Set the global volume
sessions
  .find((session) => session.master)
  ?.setVolume(0.1);

// Release native handlers
sessions.forEach((session) => session.cleanup());
```
