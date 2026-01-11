# 3.3 V Linear Regulator Spice Directives

## Steady-State Analysis Directives
```spice    
; ---------- Include Libraries ----------
.inc TIP42C.lib
.inc LM358.lib
 
; ---------- Parameters ----------
.param Vs=5     ; Supply voltage
.param iL=12m  ; Load current
.param ref=1.6k ; Reference resistor
.param base=2.7k ; Base resistor
.param pull=10k ; Pull-up resistor
.param sense=0.22 ; Sense resistor
.param FB1=10k ; Feedback resistor 1
.param FB2=30.1k ; Feedback resistor 2
.param Cout=300uF ; Output capacitor
 
; ---------- Analysis ----------
;.op
.tran 0 100m 0 100u
;.ac dec 100 1 1e6
 
; --- Pulse Load Transient Analysis ---
; Replace {iL} parameter for ILoad with pulse definition
;PULSE(12m 120m 10m 100n 100n 120u 3m) ; Load current pulse

; ---------- Scaled Measurements ----------
;* Define unit prefixes
.param u=1e6 ; micro
.param m=1e3 ; milli
.param k=1e-3 ; kilo

;* steady-state measurements
.meas OP Vout PARAM V(collector)
.meas OP Vdropout PARAM V(emitter)-V(collector)
.meas OP Vref PARAM V(OpAmp_neg)
.meas OP I_Ref_mA PARAM Ix(U2:K)*m
.meas OP I_BJT_base_uA PARAM -Ib(Q1)*u
.meas OP I_BJT_emitter_mA PARAM Ie(Q1)*m
.meas OP I_BJT_collector_mA PARAM -Ic(Q1)*m
.meas OP Beta_BJT PARAM Ic(Q1)/Ib(Q1)


; ---------- Sweeps / Corners (optional) ----------
;.step param Vs 4 7 0.5         ; Supply voltage sweep
;.step param ref 200 2.2k 50    ; Reference resistor sweep
;.step param base 1k 5k 500     ; Base resistor sweep
;.step param sense 0.1 1 0.1    ; Sense resistor sweep
;.step param iL 0 120m 10m      ; Load current sweep
;.step param Cout 10u 470u 50u  ; Output capacitor sweep
```

## Transient Analysis Directives

Change the value of the load current source to a pulse for transient analysis:
```spice
;PULSE(12m 120m 10m 100n 100n 120u 3m) ; Load current pulse
```