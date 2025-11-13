# recruit-vicharak
A simple Class-D amplifier designed in KiCad
It turns an analog audio signal into a fast on/off waveform (PWM), switches power through MOSFETs (or transistor stages), then uses an LC filter to convert the PWM back into sound for a speaker.
Components 
LM393 (comparator): Compares the audio signal with a triangle (carrier) wave. When audio is higher than the triangle the output goes high; otherwise it goes low. That makes the PWM.

BC107 (NPN transistor): Can be used to drive gates or to create a simple push‑pull driver stage when you don’t use MOSFET gate drivers. It’s a small signal transistor — good for logic-level switching at low current.

Resistors: Set gains, comparator hysteresis (thresholds), limit currents to transistor bases/gates and form RC timing with capacitors.

Inductor + Capacitor (LC filter): Smooth the PWM into audio — the inductor resists sudden current changes, and the capacitor holds voltage — together they filter out the high switching frequency and leave the audio.

Why these choices are OK for a simple build

LM393 is common and made for comparators — it’s perfect for creating PWM from audio + triangle generator. It runs on a single supply and has an open‑collector output which makes level shifting easy.

BC107 is a cheap, easy-to-find transistor for small driver functions (e.g., buffering comparator output, making small delays, or forming part of a simple totem‑pole driver). For higher power switching you’d still want MOSFETs, but BC107 is fine for low‑power tests.

Resistors, inductors and capacitors are the basic building blocks — simple and reliable.

BLOCK FLOW
Audio input → small preamp or buffer (sets volume).

Triangle/oscillator (made with op‑amp or simple RC relaxation) → 250 kHz or lower depending on parts.

LM393 compares audio vs triangle → produces PWM signal.

BC107 stages may buffer or translate LM393 outputs to drive power switches.

Power switching stage (if you used MOSFETs on the KiCad board: they switch the supply to the speaker) — if you used transistors instead, their arrangement controls the speaker current directly.

LC filter between the switching nodes and speaker → smooths PWM to audio.

How to simulate 

KiCad + ngspice: You can run a transient simulation inside KiCad (Eeschema with ngspice). Replace LM393 with an ideal comparator model or use an op‑amp model configured as comparator. For BC107 use an NPN model (2N2222/BC107) available in SPICE libraries.

What to watch in simulation: triangle shape, PWM waveform, switching node voltages, LC filter output, current through switches.
