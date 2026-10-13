Convertor Binar - Gray pe 8 Biți (FPGA BASYS 3)
Proiect de Electronică Digitală realizat în cadrul Facultății de Automatică și Calculatoare, Universitatea Tehnică „Gheorghe Asachi” din Iași. Modulul implementează un convertor de cod Binar - Gray pe 8 biți în limbaj VHDL, sintetizat și testat pe placa de dezvoltare Digilent BASYS 3 cu FPGA Xilinx Artix-7.
Autori:
  Ghidescu Dragoș-Ioan
  Ostaci Ionuț
  Coordonator proiect: Asist. Drd. Marius Obreja
Descriere Generală și Funcționalități:
Modulul preia o valoare binară de intrare pe 8 biți și calculează codul Gray corespunzător conform relațiilor logice:
•	G(7)=B(7)
•	G(i)=B(i)⊕B(i+1) pentru i=6-0

Caracteristici principale:
  Introducere date: Valoarea binară de intrare este setată prin comutatoarele sw(0..7)
  Control sincronizat al conversiei: Actualizarea rezultatului este condiționată de comutatorul load (SW15) și de un semnal manual de ceas clk_ext generat prin apăsarea butonului central.
  Afișare binară și Gray pe LED-uri: LED-urile led(0..7) reflectă valoarea binară introdusă, iar LED-urile led_gray(0..7) (LED-urile 8–15 ale plăcii) indică rezultatul conversiei în cod Gray.
  Afișare zecimală pe 7 segmente: Valoarea binară pe 8 biți (între 0 și 255) este convertită în format BCD și afișată în zecimal pe display-ul cu 7 segmente prin multiplexare temporală.

Arhitectură Hardware și Implementare VHDL:
  Proces de conversie BCD: Utilizează funcțiile to_integer și to_unsigned din biblioteca IEEE.NUMERIC_STD pentru a descompune valoarea de 8 biți în trei cifre individuale (digit0, digit1, digit2) prin operații de împărțire și modulo (mod 10, /10 mod 10, /100 mod 10).
  Divizor de frecvență: Un numărător pe 20 de biți (refresh) alimentat de ceasul intern de 100 MHz (clk_int) reduce frecvența la aproximativ 95 Hz (perioadă de 10.48 ms), frecvență optimă pentru multiplexarea anozilor fără scintilații vizibile.
  Multiplexor 4:1: Folosește biții de selecție sel <= refresh(19 downto 18) pentru activarea succesivă a fiecărui anod (an(3 downto 0)) și transmiterea cifrei corespunzătoare la decodor.
  Decodor pentru afișajul cu 7 segmente: Convertește valoarea cifrei curente (0–9) în semnalele catodice active pe nivel coborât seg(6 downto 0).
  Registru de conversie Gray: Proces sincronizat pe frontul crescător al clk_ext care execută algoritmul Gray doar când semnalul load este activ ('1').

Simulare și Testare:
  Testbench în Vivado: Funcționalitatea logică a fost validată prin simulare comportamentală.
  Ajustare pentru simulare: Pentru a reduce durata simulării sub 100 de perioade de ceas intern, biții de selecție ai multiplexorului au fost temporar comutați pe refresh(3 downto 2), scurtând ciclul de reîmprospătare la 32 de perioade (320 ns).
  Stimuli testați: Au fost simulate tranzițiile pentru valorile 6 (00000110) și 12 (00001100), verificându-se fronturile crescătoare pe clk_ext și activarea semnalului load.
  Testare pe placă fizică: Bitstream-ul generat a fost încărcat pe placa BASYS 3, validându-se corectitudinea conversiei și a afișajului zecimal pentru valori precum 6, 38, 90, 100, 114 și 160.
  
Mediu de Dezvoltare și Referințe:
  Mediu de sinteză și simulare: Xilinx Vivado Design Suite
  Platformă hardware: Placa Digilent BASYS 3 FPGA (Artix-7 xc7a35tcpg236-1)
  Referințe: IEEE Standard VHDL Language Reference Manual și Ghidul de referință Digilent BASYS 3.

Poze reprezentative:
  <img width="1431" height="570" alt="Simulare" src="https://github.com/user-attachments/assets/a3e60deb-61e8-48f6-aef6-e8390fede379" />\
  <img width="1377" height="992" alt="Functionalitate1" src="https://github.com/user-attachments/assets/6b35d6d8-d53a-42b4-b5ea-c57981cd464b" />
  <img width="1458" height="969" alt="Functionalitate2" src="https://github.com/user-attachments/assets/098fa0c8-9959-4420-9457-3fc42e6a8170" />


