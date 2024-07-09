## 1. Kaj je RxJS?
## 2. Pojasnite koncept opazovalcev (Observables) v RxJS.

**Opazovalci (Observables)** so osrednji koncept v RxJS (Reactive Extensions for JavaScript), kar je knjižnica za reaktivno programiranje z uporabo opazovalcev. Opazovalci predstavljajo zaporedje dogodkov ali vrednosti skozi čas, kar omogoča razvijalcem učinkovito upravljanje asinhronih podatkovnih tokov.

### Ključni koncepti opazovalcev:
1. **Proizvajalec**: Vir podatkov, ki ustvarja vrednosti skozi čas. To je lahko karkoli, od uporabniških vnosov, zahtevkov na spletne storitve do drugih asinhronih podatkovnih tokov. 
2. **Potrošnik**: Naročnik ali opazovalec, ki porabi vrednosti, ki jih oddaja opazovalec.

### Življenjski cikel opazovalca:
1. **Ustvarjanje**: Opazovalec je ustvarjen z uporabo različnih metod, ki jih ponuja RxJS.
2. **Naročnina**: Opazovalci se naročijo na opazovalca, da začnejo prejemati podatke.
3. **Izvajanje**: Opazovalec začne proizvajati vrednosti in jih pošilja naročnikom.
4. **Dokončanje/Napaka**: Opazovalec se dokonča ali naleti na napako, kar konča podatkovni tok.

### Prednosti opazovalcev:
- **Asinhrono upravljanje**: Enostavno upravljanje asinhronih podatkovnih tokov.
- **Sestavljivost**: Uporaba operaterjev za kombiniranje več opazovalcev ali transformacijo podatkov.
- **Leno izvajanje**: Opazovalci se ne izvajajo, dokler niso naročeni, kar jih naredi učinkovite.
- **Prekinitev**: Naročnine je mogoče enostavno preklicati in ustaviti pretok podatkov.

## 3. Kako ustvarite opazovalca (Observable) v RxJS?
## 4. Kaj so operaterji v RxJS?
## 5. Razlikujte med cevovodnimi (pipeable) in ustvarjalnimi (creation) operaterji v RxJS.
## 6. Pojasnite namen funkcije pipe v RxJS.
## 7. Kakšna je razlika med mergeMap in switchMap?
## 8. Kako se concatMap razlikuje od mergeMap?
## 9. Kakšen je namen operaterja filter v RxJS?
## 10. Kako uporabljate operater map v RxJS?
## 11. Pojasnite operater tap v RxJS.
## 12. Kaj je operater catchError in kako se uporablja?
## 13. Kako obravnavate napake v RxJS?
## 14. Pojasnite namen operaterja retry.
## 15. Kakšna je razlika med of in from v RxJS?
## 16. Kako uporabljate operater combineLatest?
## 17. Kakšen je namen operaterja forkJoin v RxJS?
## 18. Kako uporabljate operater zip v RxJS?
## 19. Pojasnite operater withLatestFrom v RxJS.
## 20. Kaj je subjekt (Subject) v RxJS?
## 21. Razlikujte med Subject, BehaviorSubject in ReplaySubject.
## 22. Kako multicastirate opazovalca (Observable) v RxJS?
## 23. Kakšen je namen operaterja share?
## 24. Kako debounce-ate uporabniški vnos v RxJS?
## 25. Pojasnite operater debounceTime v RxJS.
## 26. Kako throttle-ate uporabniški vnos v RxJS?
## 27. Kakšen je namen operaterja throttleTime?
## 28. Pojasnite operater distinctUntilChanged.
## 29. Kako implementirate anketiranje (polling) z RxJS?
## 30. Kaj je operater expand v RxJS?
## 31. Kako upravljate stanje z RxJS v Angular aplikacijah?
## 32. Kakšen je namen operaterja take v RxJS?
## 33. Pojasnite operater takeUntil.
## 34. Kako uporabljate operater takeWhile?
## 35. Kaj je operater first v RxJS?
## 36. Kako uporabljate operater last v RxJS?
## 37. Pojasnite operater scan.
## 38. Kakšen je namen operaterja reduce?
## 39. Kako uporabljate operater delay v RxJS?
## 40. Pojasnite operater startWith.
## 41. Kakšen je namen operaterja endWith?
## 42. Kako uporabljate operater repeat v RxJS?
## 43. Pojasnite operater pairwise.
## 44. Kako uporabljate operater window v RxJS?
## 45. Kaj je operater buffer v RxJS?
## 46. Kako združujete opazovalce (Observables) v RxJS?
## 47. Pojasnite operater merge.
## 48. Kaj je operater concat v RxJS?
## 49. Kako obravnavate sočasnost (concurrency) v RxJS?
## 50. Katere so najboljše prakse za uporabo RxJS z Angularjem?
## 51. Pojasnite razliko med hladnimi (cold) in vročimi (hot) opazovalci.
## 52. Kako uporabljate urnike (schedulers) v RxJS in kakšen je njihov namen?
## 53. Kaj so višjeredni opazovalci (higher-order Observables) v RxJS?
## 54. Kako ustvarite lastne operaterje v RxJS?
## 55. Pojasnite razliko med concatMap, mergeMap in switchMap podrobno.
## 56. Kako uporabljate operater groupBy v RxJS?
## 57. Pojasnite koncept povratnega pritiska (backpressure) v RxJS.
## 58. Kako obravnavate velike tokove podatkov v RxJS?
## 59. Kako integrirate RxJS z Redux ali NgRx?
## 60. Kakšen je namen operaterjev materialize in dematerialize?
## 61. Kako testirate opazovalce (Observables) v RxJS?
## 62. Pojasnite koncept reaktivnega programiranja in kako RxJS to omogoča.
## 63. Kako uporabljate operater exhaustMap v RxJS?
## 64. Kako obravnavate zapletene asinhrone poteke dela z RxJS?
## 65. Katere so prednosti uporabe RxJS pred tradicionalnimi metodami asinhronega obravnavanja, kot so povratni klici (callbacks) in obljube (promises)?
## 66. Kako uporabljate operater race v RxJS?
## 67. Pojasnite koncept multicastinga z ConnectableObservable.
## 68. Kako implementirate eksponentno povečevanje z RxJS?
## 69. Kako obravnavate ponovitve z zamudami v RxJS?
## 70. Kako uporabljate operaterja audit in auditTime v RxJS?
## 71. Kakšen je namen operaterja partition v RxJS?
## 72. Kako obravnavate dinamične tokove v RxJS?
## 73. Kako uporabljate operaterja sample in sampleTime?
## 74. Pojasnite koncept debounce-a in throttle-a v RxJS.
## 75. Kako implementirate funkcionalnost povleci in spusti (drag and drop) z RxJS?