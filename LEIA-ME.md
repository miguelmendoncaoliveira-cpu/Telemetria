# App de Telemetria — versão 4

App web (PWA) que liga ao HM-10 por **Web Bluetooth**. Funciona no **Chrome do Android**, no **Chrome/Edge do PC** e no iPhone com o browser **Bluefy**.

## Ficheiros

| Ficheiro | O que é |
|---|---|
| `index.html` | A app toda |
| `sw.js` | Service worker: guarda a app no telemóvel para abrir **sem internet** |
| `manifest.webmanifest` | Nome, ícone e cores para instalar no ecrã principal |
| `icon.svg` | Ícone |

## Modo normal — Telemetria (acento azul)

- **Instantâneo** — mostradores de rotações e velocidade ao centro; água e turbo à esquerda; força G e consumo à direita. Por baixo, os **canais** em quatro secções (Motor · Turbo e consumo · Dinâmica · Habitáculo e GPS), com valor, mínimo e máximo, e o gráfico de 5 faixas dos últimos 2 minutos.
- **Botão Gravar (canto superior direito)** — cronómetro a contar; **pausa** para parar o tempo e depois **Continuar**, **Guardar** (vai para o Histórico) ou **Descartar** (pede confirmação). Enquanto grava, desliza para o lado (ou toca em *Gravação*) para ver distância, tempos, consumo, percurso e gráficos da viagem.
- **Histórico** — viagens gravadas: estatísticas, percurso, gráficos, renomear, exportar CSV, apagar.
- **Ligação** — HM-10, modo demo, alarmes, Racing, acelerómetro, diagnóstico.

## Ecrã de ligação
Ao abrir a app aparece só o ecrã **Ligar ao carro**: toca no botão, escolhe o HM-10 e, quando a ligação fica feita, aparece "LIGADO" e a telemetria desbloqueia. Se a ligação cair a meio, a app religa sozinha sem bloquear (e nunca tapa uma gravação a decorrer); só volta a este ecrã quando desligas de propósito. Há também um atalho para o modo demo.

## Modo Racing (interruptor RACING, acento vermelho)

Ao ligar o interruptor há uma transição e a barra lateral passa a vermelho, com:

- **Corrida** — barra de rotações por segmentos (branco → zona de mudança verde/amarelo/vermelho → azul a piscar no limite); linha de tempos com **cronómetro da volta** e **delta** em destaque, última, melhor, setores e voltas; RPM, km/h (com mudança estimada) e **mapa do circuito** em grande; em baixo água, turbo, G, combustível, consumo e estado. Nada é cronometrado até carregares em **Gravar sessão**: há um countdown (luzes · 3 · 2 · 1 · GO) e o ponto onde estás passa a ser a meta. Botão **ECRÃ INTEIRO** para esconder a barra lateral (sai com Esc ou duplo toque).
- **Botão Gravar sessão** — o mesmo controlo no topo; as voltas completas (fora da pausa) ficam guardadas. Desliza para o lado para ver tempos por volta, tabela e circuito. Não dá para mudar de modo com uma gravação ativa.
- **Histórico** — sessões de corrida: melhor volta, volta teórica, gráfico e tabela de voltas (roxo = melhor), circuito, exportar CSV, apagar.
- **Ligação** — as mesmas definições.

## Pôr online (GitHub Pages)

1. No repositório `telemetria` do GitHub: **Add file › Upload files** → os 4 ficheiros → Commit.
2. **Settings › Pages** → branch **main** / **(root)** → Save.
3. Abrir `https://<utilizador>.github.io/telemetria/` no Chrome do Android → menu ⋮ → **Instalar app**.

Na primeira abertura com internet a app fica guardada; a partir daí abre mesmo sem rede. No Android, a **Localização** tem de estar ligada para a pesquisa Bluetooth encontrar o HM-10.

## Formato da trama (sem alterações)

```
$T,ms,rpm,vel,t_agua,turbo_real,turbo_pedido,inj,ax,ay,az,lat_e6,lon_e6,vel_gps,t_hab,hum*
```
Campo vazio = sem valor novo. Acelerações em mg; latitude/longitude em milionésimos de grau.
