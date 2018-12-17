INSTRUCTIONS
=======

From your terminal, please clone the "ortclib-sdk" git repository:
git clone --recursive https://github.com/ortclib/ortclib-sdk.git

This repository will yield the ORTC Lib SDK and dependency libraries.

Directory structure:

- ortc-lib-sdk\bin          	contains scripts for preparing an environment for Windows
- ortc-lib-sdk\common          contains samples applications that can use Ortc and WebRtc libraries. Currently it is only the case for PeerCC sample 
- ortc-lib-sdk\ortc    		contains code of Ortc and dependency libraries
- ortc-lib-sdk\webrtc    		contains code of WebRtc and dependency libraries
- ortc-lib-sdk\docs			contains documentation


How to Build:

WINDOWS BUILD :
----------------------------

1) Run prepare script, from your terminal:
<br />
<pre>
<code>
cd ortclib-sdk
bin\prepare.bat
</code>
</pre>
<br />
This script will prepare environment but it won't build webrtc projects. In this case webrtc project will be built from Visual Studio once you try to build Org.Ortc or Org.WebRtc.

2) From VS2015, load ortc\windows\solutions\Ortc.sln for Ortc or webrtc\windows\solutions\WebRtc.sln for WebRtc development.

3) Now you can build winuwp libraries for Ortc or WebRtc and deploy sample apps ChatterBox (WebRtc only) and PeerCC.

====

# Unity Video Rendering on HoloLens

## Unity build requirements

* Unity version 2018.2.13 (2018.2.13f1) with IL2CPP Scripting Backend

## Running Unity Peer Connection Client application on HoloLens device 

1. Open `webrtc\windows\solutions\WebRtcUnity.sln` solution, select x86 platform and build PeerConnectionClientUnityCore project. The build procedure produces WebRTC libraries, WebRTC for UWP wrapper component and deploys WebRTC and Peer Connection Client Core libraries to the Unity project space.
2. Open Unity project `common\windows\samples\PeerCC\ClientUnity' in Unity Editor
3. Go to 'File' -> 'Build settings...', select 'Universal Windows Platform', click on the 'Build' button and choose an export folder
4. Add the following XML block to generated manifest file `PeerCCUnity\Package.appxmanifest`:
```
  <Extensions>
    <Extension Category="windows.activatableClass.inProcessServer">
      <InProcessServer>
        <Path>WebRtcScheme.dll</Path>
        <ActivatableClass ActivatableClassId="WebRtcScheme.SchemeHandler" ThreadingModel="both" />
      </InProcessServer>
    </Extension>
  </Extensions>
```
5. Open PeerCCUnity.sln from export folder, build PeerCCUnity project and run the application on the device 
