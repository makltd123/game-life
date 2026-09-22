# Self-Modifying Ecosystem Simulation

**English** | [Русский](README.ru.md)

A browser simulation where agents don't just live in the world — they rewrite its rules. One HTML file, no dependencies: download `index.html` and open it in a browser.

## How it works

- **The world** is a 100×100 grid with resources and up to 500 agents. Its rules are five parameters: resource spawn rate, resource decay rate, mutation rate, gravity bias (resources drift downward) and hostility.
- **Agents** have energy and a genome of six traits (`resource_seeking`, `aggression`, `cooperation`, `reproduction_drive`, `world_influence`, `adaptability`), normalized to sum to 1. Each step an agent loses 0.3 energy and dies at zero; a resource gives +25.
- **Behavior:** a hungry agent moves toward the nearest resource; with 60+ energy it can reproduce into a free neighboring cell. The child inherits the parent's genome, and each trait mutates with probability equal to the world's current mutation rate.
- **Rewriting the rules:** an agent with more than 60 energy and older than 20 steps proposes a change to a world parameter, chosen by its genome — resource seekers push resource spawn up, cooperative agents push hostility down, aggressive ones push it up, and so on. The strength of a proposal is energy × the agent's influence score.
- **Every step** the proposals for each parameter are combined into an average weighted by strength. A higher stability index makes the world resist changes more; stability itself falls as changes pile up, hostility grows and mutation speeds up.

The UI shows the world, the current parameters and statistics: generation, population, average influence, mutation rate, system volatility and number of world changes. Controls: Play, Step, Reset and a speed slider.

## Known gaps

- Hostility does not affect agents yet: there is no fighting or other interaction. It only lowers stability and changes the background.
- The `world_influence` gene is not used: an agent's influence score is random at birth.

## License

[MIT](LICENSE)
