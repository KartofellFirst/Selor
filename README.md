<p align=center>
  <h1>
    <p align=center>
      Selor' <br>
      <img src="https://img.shields.io/static/v1?label=&message=HTML&color=orange&">
      <img src="https://img.shields.io/static/v1?label=&message=Wayland&color=green&">
      <a href="https://github.com/KartofellFirst/hotoe"><img src="https://img.shields.io/static/v1?label=&message=Hotoe&color=9999ff&"></a>
      <img src="https://img.shields.io/static/v1?label=&message=Hyprland&color=teal&">
    </p>
    <p align=center>
      <img src="gif.gif" width="300">
      <img src="gif.gif" width="300">
      <img src="gif.gif" width="300">
    </p>
  </h1>
</p>


<h3><p align=center>Hyprland lockscreen built using HTML</p></h3>
<p align=center>
  <a href="https://github.com/user-attachments/assets/0d7c5647-472a-4a94-958e-7bc422fa57c5">full demo</a><br><br>
  <sub>why it's different ↓</sub><br>
  <a href="#how-it-works">how the backend works</a><br><br>
  <sub>how to get ↓</sub><br>
  <a href="#configuration">customisation</a><br>
  <a href="#requirements">requirements</a><br>
  <a href="#usage">usage</a><br>
</p>
<br><br><br><br><br><br><br><br><br><br>


## requirements:
+ [hotoe](https://github.com/KartofellFirst/hotoe)
+ Hyprland (Latest versions of)

<p align=center><a href="#hyprland-lockscreen-built-using-html">back</a></p>
<br><br><br><br>

## How it works
Calling *Selor* activates a sequence of hyprctl calls. <br>
<details><summary>which ones? (click)</summary>
  <code>hyprctl activeworkspace -j | jq '.id'</code> — gets and saves current focused worspace <br>
  <code>id=$(hyprctl workspaces -j | jq '[.[].id] | max + 1'); hyprctl eval "hl.dispatch(hl.dsp.focus({ workspace = '$id' }))"</code> — Finds a free workspace with no windows to demonstrate your wallpapers<br>
  <code>hyprctl activeworkspace -j | jq '.id'</code> — saves the free workspace index <br>

  <b>then</b> <br>
  each 100ms it focuses free workspace again, protecting from focusing your opened apps and somehow opening new windows (idk why it just works like that). <br>
  You cant type anywhere or open anything until you login <hr><br>
</details>

It does **not** draw a window in **session_lock_layer** as many other lockscreens do. This approach has several vulnerabilities and advantages: <br>

**Pros:**
+ doesn't freeze your session (your apps will keep working without thread to be interrupred. Great to protect long-term processes: renders, compilations, etc)
+ it actually can show your wallpapers on your lockscreen (many other utilities demand setting them up separately)

**Vulnerabilities:**
- exits to tty (Ctrl + Alt + F*) are still working, able to ruin your running processes
- Hyprland keybinds are still one level higher, means if you have something like "bind SUPER+X -> rm -rf", it will happen <br> (or more usual "bind SUPER+M -> exit to logged-in tty" (just call start-hyprland and you bypassed the lock))

_(You better consider adding some flags to disable these kind of binds when the Selor is running to have full protection)_

<p align=center><a href="#hyprland-lockscreen-built-using-html">back</a></p>
<br><br><br><br>


## configuration
Because Selor is built with HTML, it's highly customizable. Every free AI can help you with that if you don’t know frontend yourself, because it's that easy<br>
You can:
- Add sounds / pictures / videos / mini-games / widgets
- Remove everything or rewrite as you think it will be better

In the current code you can setup:
`WAIST_RATIO` — How thin the star is<br>
`PHASES` — duration of each intro phase<br>
<br>
`CONFIG.enabled` — enable outro
`CONFIG.lingering` — delay after login (if set to 0 you'll be seeing your workspace switching back to normal animation)
<br>
`STEPS` — outro animation steps
<br>
`LIFETIME` — drawing line lifetime before disappearing
`spacing` — how densely to fill the gap when you draw (higher => less dense => easier for your GPU)

<p align=center><a href="#hyprland-lockscreen-built-using-html">back</a></p>
<br><br><br><br>

