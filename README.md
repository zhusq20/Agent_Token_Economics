# Agentic AI Systems Should Be Designed as Marginal Token Allocators

📄 [**Read the paper (PDF)**](paper.pdf) &nbsp;·&nbsp; 🌐 [**Project page**](https://zhusq20.github.io/Agent_Token_Economics/)

---

## TL;DR

Routers, agents, serving stacks, and trainers look like four different engineering problems. They are not. They are four readings of **one allocation problem**, evaluated at four shadow prices that today no single layer can see.

The system should spend the next token on:

$$
i^{*} = \arg\max_{i}\Big[V\,\Delta Q_i - \Delta C_i - \lambda\,\Delta L_i - \rho\,\Delta R_i\Big]
$$

where $V$ is task value, $\Delta C_i$ is marginal compute cost, $\lambda$ is the shadow price of latency, and $\rho$ is the shadow price of risk.

## The four layers

| Layer | Mechanism | Index | Prices observed |
|---|---|---|---|
| Demand | Routing as screening | model tier | $V$, $\Delta C_i$ |
| Action | Agent as principal–agent | plan / act / verify | $\rho$, $V$ |
| Supply | Serving as production | prefill / decode / KV | $\lambda$, $\Delta C_i$ |
| Capital | Caches & RL as investment | rollout / store | $\Delta C_i$, $\rho$ |

## Predicted failure modes

The unified view turns failures into corner cases of one equation: **over-routing**, **under-routing**, **over-delegation**, **under-verification**, **serving congestion**, **stale RL rollouts**, and **cache misuse**.

## Design implications

1. **Token-aware evaluation** — report all four prices, not just dollar cost.
2. **Risk-adjusted routing** — publish a regret bound or an incentive-compatible menu.
3. **Autonomy pricing** — make action class explicit; price irreversible actions higher.
4. **Congestion-priced serving** — expose shadow prices for prefill / decode / KV.
5. **RL token budgeting** — equalize marginal capability gain across rollouts, verifiers, and updates.

## Citation

```bibtex
@misc{zhu2026marginaltoken,
  title  = {Agentic AI Systems Should Be Designed as Marginal Token Allocators},
  author = {Siqi Zhu},
  year   = {2026},
  note   = {Position paper, preprint}
}
```

## License

The website source (HTML/CSS) is released under the MIT license. The paper itself is © 2026 Siqi Zhu, all rights reserved (preprint distribution permitted).
