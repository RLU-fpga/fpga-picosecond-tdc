# Pikosekundinis optinis laiko-skaitmeninis keitiklis (TDC) ir optinis bandymų stendas

Aparatinės įrangos ir programuojamos logikos platforma, skirta itin trumpų optinių impulsų laiko intervalų matavimui pikosekundžių skyra. Sistema apima sparčią optinio siųstuvo grandinę, plačiajuostį transimpedansinį imtuvą, mažo f法の drebėjimo (angl. *low-jitter*) sąsajos logiką ir FPGA pagrindu realizuotą atsišakojančių vėlinimo linijų (angl. *tapped delay line*, TDL) TDC architektūrą „AMD/Xilinx Zynq-7000“ SoC luste.

Fizinė optikos ir jutiklių sistema sumontuota ant standaus aliuminio profilio bėgio stendo, užtikrinančio mikronų lygio optinio spindulio justavimą, mechaninį slopinimą bei atkartojamus skrydžio laiko (angl. *Time-of-Flight*, ToF) matavimus.

---

## Pagrindinės savybės ir sistemos architektūra

* **Optomechaninis bandymų stendas:**
  * Optinis traktas ir optoelektronika sumontuoti ant standaus aliuminio ekstruzijos profilio bėgio, eliminuojant mechaninį laisvumą ir vibracijų sukeliamą laikinį drebėjimą (*jitter*).
  * Tikslus atstumo tarp siųstuvo ir detektoriaus reguliavimas, skirtas sisteminiam skrydžio laiko (ToF) ir optinio kelio vėlinimo parametrų nustatymui.

* **Spartus optinis siųstuvas:**
  * GaN FET tranzistoriais („EPC2016“) valdomas nanosekundinių / subnanosekundinių impulsų lazerinis siųstuvas (450 nm).
  * Nanosekundinis impulsų valdiklis („LMG1020“), sukonfigūruotas itin dideliam signalo augimo greičiui (*slew rate*) ir minimaliam valdymo-į-šviesą sklidimo vėlinimui.

* **Analoginė priėmimo dalis ir imtuvas (AFE):**
  * Plačiajuostis fotodiodas, sujungtas su itin sparčiu transimpedansiniu stiprintuvu („OPA855“, ~8 GHz GBW), užtikrinančiu tikslų trumpų impulsų atkūrimą.
  * Greitaeigio diferencialinio diskriminatoriaus pakopa („TLV3601“ / PECL lygio formavimas per „MC100“ seriją), formuojanti švarius START / STOP loginius frontus su minimaliu triukšmu.

* **FPGA logika ir vėlinimo linijų branduolys („Digilent Arty Z7-20“ / „Zynq-7020“):**
  * Aparatinė atsišakojanti vėlinimo linija (TDL), išnaudojanti vidinius FPGA greitosios pernašos loginius elementus (`CARRY4`), leidžianti taktinio signalo periodą diskretizuoti į pikosekundinės eilės laiko intervalus (*bins*).
  * Realaus laiko intervalų kalibracija, termometrinio kodo dekodavimas į dvejetainį ir „burbulų“ klaidų (angl. *bubble errors*) šalinimas.
  * Telemetrijos srauto perdavimas per UART sąsają į kompiuterį tolesniam duomenų apdorojimui ir statistinei analizei.

* **Maitinimo ir signalų vientisumas:**
  * Daugiapakopis itin mažo triukšmo LDO maitinimo paskirstymas („Texas Instruments LP38798“) su atskirtomis analoginėmis, optinėmis ir skaitmeninėmis grandinėmis, siekiant minimizuoti parazitinius taktinių dažnių trikdžius bei fazinį triukšmą.
