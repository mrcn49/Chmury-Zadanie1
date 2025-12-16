# CZĘŚĆ OBOWIĄZKOWA

## Utworzenie klastra
<img width="811" height="168" alt="image" src="https://github.com/user-attachments/assets/6782aafb-0047-4408-9500-584acd169fac" />

## Labelowanie węzłów
<img width="798" height="258" alt="image" src="https://github.com/user-attachments/assets/66dd93c4-7087-435d-a7a6-64f64987241e" />

## Aplikacja manifestów
<img width="650" height="585" alt="image" src="https://github.com/user-attachments/assets/02560e1c-87b3-48d2-9ff9-69af0ac436eb" />


## Spis podów
<img width="994" height="506" alt="image" src="https://github.com/user-attachments/assets/9c7a5444-70fb-438e-a2c2-525d3e85c99a" />

## Stworzenie podów do testów 
<img width="982" height="101" alt="image" src="https://github.com/user-attachments/assets/43e956af-b4a7-4784-8580-cea7e58bdad2" />

## Wynik
<img width="996" height="568" alt="image" src="https://github.com/user-attachments/assets/367de258-3f40-4421-b400-5d20ed1de10e" />

## Testowanie polityki sieciowej
<img width="1140" height="251" alt="image" src="https://github.com/user-attachments/assets/eb551b91-bf9b-4128-bb22-7560f8877e66" />

<img width="1157" height="101" alt="image" src="https://github.com/user-attachments/assets/f27aa69e-fb6f-4e83-9a44-2cfffee3f260" />

<img width="1157" height="101" alt="image" src="https://github.com/user-attachments/assets/4f6d7216-21cd-47f9-8ee4-729552c9b93b" />

<img width="1157" height="101" alt="image" src="https://github.com/user-attachments/assets/33e4e51f-72f4-4e66-8f58-b5803fdd2b51" />

## Test obciążenia
<img width="889" height="269" alt="image" src="https://github.com/user-attachments/assets/654ca24a-fd37-4000-942f-009066ea7044" />

<img width="892" height="212" alt="image" src="https://github.com/user-attachments/assets/7a61ba66-868e-4083-8150-5647dfd41965" />

# CZĘŚĆ NIEOBOWIĄZKOWA

1. **Tak** - https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#migrating-deployments-and-statefulsets-to-horizontal-autoscaling

2. **Parametry RollingUpdate i konfiguracja**
Strategia aktualizacji: Należy ustawić w Deployment następujące wartości:
```
maxSurge: 0
maxUnavailable: 1
```
**Uzasadnienie:** 

**maxSurge: 0** jest konieczny, aby przy maksymalnym wyskalowaniu nie próbować utworzyć nadmiarowego poda, co naruszyłoby ResourceQuota. 

Z kolei **maxUnavailable: 1** zapewnia płynną wymianę podów "jeden za jeden", minimalizując spadki dostępności.

Należy ustawić w HPA parametr **minReplicas: 3**. Jest to niezbędne, ponieważ przy dozwolonej niedostępności jednego poda, musimy mieć minimum 3 repliki, aby zawsze zagwarantować działanie wymaganych dwóch

Możemy  ustawić **maxReplicas** na równi z limitem ResourceQuota (5), co pozwala na maksymalne wykorzystanie zasobów klastra bez ryzyka przekroczenia limitów podczas wdrażania zmian.
