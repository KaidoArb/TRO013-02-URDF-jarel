**Küsimused:**
1. **Mitu lüli (link) on Yahboom roboti mudelis?**
Vastus: Kokku on 10 link'i. 6 tavalist link'i ja 4 Xacro laienduse abil loodud link'i.
   - Vihje: loenda kõik `<link name="...">` elemendid. Ära unusta `base_footprint`-i!
   - Lisavihje: `grep -c '<link name=' /tmp/robot.urdf` (pärast xacro teisendust)
2. **Mitu liigest (joint) on?**
Vastus: Kokku on 9 joint'i. Joint ühendadab erinevaid link'e mis tähendab, et joint'e on alati vähem kui link'e.
   - Vihje: loenda kõik `<joint name="...">` elemendid
   - Matemaatiline kontroll: linke peaks olema liigestest ühe võrra rohkem (miks?)
3. **Mis tüüpi on ratta liigesed? Miks just see tüüp?**
Vastus: Ratta joint'id on 'continuous', sest 'fixed' ei lubaks neil liikuda ja 'revolute' kasutab piirdeid.
   - Vihje: otsi `type="..."` ratta jointide juures
   - Mõtle: kas rattal on pöörlemisele piir (min/max nurk)?
4. **Mis vahe on `visual` ja `collision` geomeetrial?**
Vastus: Visual - igasugused visuaalsed detailid nagu detailne kuju või erinevad värvid, mida kasutatakse mudeli välimuse jaoks.
        Collision - lihtsam kuju (nt kast, silinder, kera), mida kasutatakse kokkupõrgete arvutamiseks. 
        Lihtsamate kujundite kasutamine muudab simulatsiooni kiiremaks.
   - Vihje: võrdle `base_link` visual ja collision sektsioone
   - Lisa: miks võib collision olla lihtsam?
5. **Miks on `base_footprint` eraldi `base_link`-ist?**
Vastus: Base_link - kirjeldab roboti tegelikku põhiraami koos kõrguse ja kaldega, mida kasutatakse roboti füüsilise asendi määramiseks.  
        Base_footprint - roboti projektsioon maapinnale ilma kõrguse ja kallutuseta, mida kasutatakse peamiselt navigeerimisel ja 2D liikumise arvutamisel. 
        Nende eraldamine teeb roboti juhtimise ja liikumise arvutamise lihtsamaks.
   - Vihje: vaata nende vahelist jointi -- mis tüüp see on ja milline on z-nihe?
   - Mõtle: navigatsiooni seisukohalt -- kus on "robot" kaardil?

Vasta küsimustele:
1. Mis on PROTO faili roll Webots simulatsioonis? Miks ei piisa ainult URDF-ist?
Vastus: Proto faile kasutatakse robotite, sensorite ja muude simulatsiooniobjektide defineerimiseks. URDF kirjeldab peamiselt roboti     kinemaatilist struktuuri: linke, liigendeid, massi ja visuaalset mudelit ning ei sisalda paljusid Webotsi simulatsiooniks vajalikke omadust, nagu simulatsioonis kasutatavaid sensoreid ja nende parameetreid, kontakt- ja füüsikamudeli seadeid, materjale ja renderdusomadusi, Webotsi-spetsiifilisi kontrollereid ja laiendusi.
2. Mis tüüpi infot URDF Webots-kontekstis annab? (Vihje: TF, teemade nimed)
Vastus: Linke, liigendeid, geomeetriat, inertsiaalseid omadusi, visuaalseid omadusi, kokkupõrkegeomeetriat.
3. Kui sa tahaksid muuta roboti välimust (värvi, kuju) Webotsi simulatsioonis, kas muudaksid URDF-i või PROTO-t? Miks?
Vastus: PROTO-faili, sest see kontrollib otseselt roboti visuaalset esitust simulatsioonis. URDF-i tuelks muuta pigem siis, kui on vaja muuta roboti põhimudelit või mehaanilist ülesehitust.