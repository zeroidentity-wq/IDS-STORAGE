# Jurnal de învățare — IDS-RS

Acest fișier urmărește progresul în învățarea Rust și programare prin proiectul IDS-RS.
Claude Code îl citește automat — contextul de învățare este portabil oriunde e clonat repo-ul.

---

## Profilul cursantului

- **Nivel programare:** Bazele unui limbaj (variabile, funcții, bucle)
- **Nivel rețelistică:** Concepte de bază (a auzit de IP, port, TCP/UDP)
- **Timp disponibil:** 4-7 ore/săptămână
- **Scop:** Înțelegerea profundă, nu memorarea sintaxei. Vrea să gândească ca un programator.
- **Limbă preferată:** Română

---

## Curriculum complet

```
FAZA 0  — Cum gândește un programator
FAZA 1  — Cum comunică calculatoarele (rețele, UDP, porturi, syslog)
FAZA 2  — Rust: tipuri, variabile, funcții
FAZA 3  — Rust: Ownership (conceptul central, unic în Rust)
FAZA 4  — Rust: Structs, Enums, Pattern Matching
FAZA 5  — Rust: Traits (contracte și polimorfism)
FAZA 6  — Rust: Error handling (Option, Result, operatorul ?)
FAZA 7  — Proiect: Parserul (citești și interpretezi text)
FAZA 8  — Proiect: Detectorul (algoritmi, structuri de date, sliding window)
FAZA 9  — Rust: Async și concurență (tokio, Arc, DashMap)
FAZA 10 — Proiect: Alerter + main (pui totul cap la cap)
FAZA 11 — Rescrie IDS-RS de la zero (testul final)
```

---

## Progres

### ✅ FAZA 0 — Cum gândește un programator
**Predat în sesiunea:** 2026-02-19

**Concepte explicate:**
- Ce este un algoritm și cum gândești în pași
- Descompunerea problemelor (IDS-RS împărțit în 5 probleme mici)
- Pseudocod — gândești înainte să scrii cod

**Exerciții date:**
- [ ] **0.1** — Scrie pseudocod: găsește IP-ul cu cele mai multe porturi unice dintr-un fișier de log-uri
- [ ] **0.2** — Citește `detector.rs:process_event` și răspunde: ce primește, ce returnează, ce verifică?

---

### ✅ FAZA 1 — Cum comunică calculatoarele
**Predat în sesiunea:** 2026-02-19

**Concepte explicate:**
- Adrese IP și porturi (analogia: casă + ușă)
- UDP vs TCP (carte poștală vs telefon)
- Ce este syslog și cum trimite firewall-ul log-uri
- Ce este un port scan și de ce e periculos
- Anatomia unui log Checkpoint Gaia

**Exerciții date:**
- [ ] **1.1** — `ss -tlnp` în terminal: ce porturi sunt deschise pe mașina ta?
- [ ] **1.2** — Trimite un pachet UDP manual la IDS-RS cu `nc -u` și observă output-ul cu `debug = true`

**Resurse recomandate:**
- [Computer Networking: A Top-Down Approach](https://gaia.cs.umass.edu/kurose_ross/online_lectures.htm) — primele 2 capitole
- [Julia Evans — Networking zine](https://wizardzines.com/zines/networking/)
- [How DNS Works](https://howdns.works/)

---

### ⏳ FAZA 2 — Rust: tipuri, variabile, funcții
**Status:** Nepredată — urmează

**Ce va acoperi:**
- Variabile și mutabilitate (`let` vs `let mut`)
- Tipuri primitive: `u8`, `u16`, `u32`, `u64`, `i32`, `f64`, `bool`, `String`, `&str`
- Funcții: parametri, valori de retur
- Control flow: `if`, `loop`, `while`, `for`
- Cum apar toate acestea în `config.rs` și `parser/mod.rs`

**Temă de pregătit (înainte de Faza 2):**
- Citește [The Rust Book — Capitolul 1-3](https://doc.rust-lang.org/book/) (gratuit online)

---

### ⏳ FAZA 3 — Rust: Ownership
**Status:** Nepredată

**Ce va acoperi:**
- Stack vs Heap — unde trăiesc datele
- Regula ownership: fiecare valoare are un singur proprietar
- Move semantics
- Borrowing: referințe imutabile (`&T`) și mutabile (`&mut T`)
- Lifetime-uri (pe scurt)
- De ce Rust nu are garbage collector și de ce e mai bine

---

### ⏳ FAZA 4 — Rust: Structs, Enums, Pattern Matching
**Status:** Nepredată

**Ce va acoperi:**
- `struct` — cum organizezi datele împreună (`LogEvent`, `Alert`)
- `enum` — tipuri cu variante (`ScanType::Fast`, `ScanType::Slow`)
- `match` — pattern matching exhaustiv
- `Option<T>` — absența valorii fără `null`
- `#[derive(Debug, Clone)]`

---

### ⏳ FAZA 5 — Rust: Traits
**Status:** Nepredată

**Ce va acoperi:**
- Ce este un trait (contract/interface)
- `impl Trait for Struct`
- Trait objects: `Box<dyn Trait>` și dynamic dispatch
- `Send + Sync` — thread safety
- Cum `LogParser` permite adăugarea de noi parseri fără să modifici restul codului

---

### ⏳ FAZA 6 — Rust: Error Handling
**Status:** Nepredată

**Ce va acoperi:**
- `Result<T, E>` — succes sau eroare
- Operatorul `?` — propagare automată
- `anyhow` — erori la nivel de aplicație
- Strategia „log and continue" vs „fail fast"
- De ce Rust nu are excepții

---

### ⏳ FAZA 7 — Proiect: Parserul
**Status:** Nepredată

**Ce va acoperi:**
- Ce înseamnă să „parsezi" text
- Regex: expresii regulate și cum se compilează o singură dată
- Key-value extraction din log-uri Gaia
- `split()`, `find()`, `strip_prefix()`
- De ce sunt doi parseri separați (Gaia și CEF)
- Exercițiu: scrie un parser simplu de la zero

---

### ⏳ FAZA 8 — Proiect: Detectorul
**Status:** Nepredată

**Ce va acoperi:**
- `HashMap` — structura de date cheie/valoare
- `Vec<T>` — array dinamic
- Algoritmul sliding window (fereastra de timp)
- De ce `DashMap` în loc de `HashMap` (concurență)
- Cooldown-ul alertelor — de ce e necesar
- Cleanup periodic — de ce memoria trebuie eliberată

---

### ⏳ FAZA 9 — Rust: Async și concurență
**Status:** Nepredată

**Ce va acoperi:**
- Thread vs async task (de ce async e mai eficient)
- `async fn` și `.await`
- `tokio` — runtime-ul care execută futures
- `Arc<T>` — shared ownership între task-uri
- `tokio::select!` — ascultă pe mai multe futures simultan
- `tokio::spawn` — lansează task-uri independente

---

### ⏳ FAZA 10 — Proiect: Alerter + Main
**Status:** Nepredată

**Ce va acoperi:**
- Format CEF complet — cum construiești un mesaj SIEM
- UDP socket efemer pentru trimitere
- SMTP async cu `lettre`
- `main.rs` ca orchestrator — cum leagă toate componentele
- `tokio::signal::ctrl_c()` — oprire grațioasă

---

### ⏳ FAZA 11 — Rescrie IDS-RS de la zero
**Status:** Nepredată

**Scopul:** Fără să te uiți la codul existent, rescrie IDS-RS pornind de la pseudocod.
Va demonstra că înțelegi cu adevărat toate conceptele, nu doar le-ai memorat.

---

## Instrucțiuni pentru Claude (la start de sesiune de învățare)

1. Citește acest fișier pentru a înțelege unde s-a ajuns.
2. Întreabă dacă cursantul a rezolvat exercițiile din faza precedentă și discută răspunsurile.
3. Continuă cu prima fază marcată ca `⏳ Nepredată`.
4. La finalul fazei, marchează exercițiile ca date și actualizează statusul la `✅`.
5. Respectă stilul mentor: explică întotdeauna de ce, nu doar ce.
