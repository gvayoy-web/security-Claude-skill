# Security Skill

Skill para Claude (Claude Code / Claude Desktop / Claude.ai con skills) que aplica una **auditoría de seguridad proporcional y con evidencia reproducible**, combinando:

- El método de autorización, verificación de capacidades y triage de la skill [`pentpest`](https://github.com/AlexaDetalles/pentpest-skill).
- Checklists de cobertura de las listas de referencia de la industria: **OWASP Top 10 (web)**, **OWASP API Security Top 10**, **OWASP Top 10 for LLM Applications**, **OWASP Mobile Top 10 + MASVS**, **OWASP Top 10 CI/CD Security Risks**, **CWE Top 25**, **OWASP ASVS** y **MITRE ATT&CK**.
- Una guía defensiva de **vectores de ataque web comunes** (clickjacking, subdomain takeover, dependency confusion, ataques a JWT, lógica de negocio/race conditions, open redirect, CSRF, HTTP smuggling, deserialización insegura, fuerza bruta, DDoS, scraping, typosquatting).
- Un checklist práctico para **proteger API keys y otros secretos** (nunca en el cliente, variables de entorno, gestores de secretos, claves restringidas por entorno, qué hacer si una clave se filtra, escaneo antes de publicar).

No incluye payloads de explotación, malware, técnicas de evasión de EDR/AV ni guías de intrusión no autorizada. El objetivo es metodología y cobertura, no un arsenal de ataque.

## Qué hace

1. Delimita el alcance y la autorización antes de tocar nada en vivo.
2. Comprueba qué herramientas/MCP existen realmente antes de usarlos (no asume nada instalado).
3. Mapea la superficie real del objetivo (web, API, móvil, LLM, CI/CD, etc.) y carga solo los checklists de cobertura relevantes.
4. Ejecuta revisión de código y/o pruebas en vivo con un presupuesto conservador, aumentando profundidad solo según evidencia.
5. Hace triage separando confirmado / no confirmado / informativo / descartado, sin inflar severidades.
6. Corrige solo si se le pide o ya está autorizado, verificando el cambio.
7. Entrega un informe directo con severidad, confianza, reproducción, impacto y referencia al marco correspondiente (CWE-xxx, OWASP Axx, API-xx, LLMxx, MASVS-xxx, CICD-SEC-x).

## Instalación

### Claude Code / Claude Desktop

Copia la carpeta de la skill a tu carpeta personal de skills:

```bash
git clone https://github.com/gvayoy-web/security-claude-skill.git
cp -r security-claude-skill/skills/security-skill ~/.claude/skills/security-skill
```

### Como plugin / skill de proyecto

Copia o referencia `skills/security-skill/SKILL.md` dentro de tu propio repositorio o marketplace de skills, siguiendo el formato estándar de skills de Claude (frontmatter `name` + `description`, seguido del cuerpo en Markdown).

## Ejemplo de uso

> "Revisa el código de esta API y dime si hay problemas de autorización, sin hacer peticiones externas."

> "Antes de subir esto a producción, revisa que no esté expuesta ninguna API key."

> "Haz un pentest autorizado de mi sitio en staging.ejemplo.com, ya tengo permiso del dueño."

## Requisitos y límites

- No requiere herramientas externas obligatorias: las herramientas de seguridad y servidores MCP son opcionales y se verifican antes de usarse.
- La skill no promete acceso a herramientas ausentes, ni resultados infalibles, ni cobertura exhaustiva.
- Las listas de referencia (OWASP, CWE, MASVS, ASVS, MITRE ATT&CK) cambian de edición periódicamente. Si el usuario pide una categoría que no aparece en `SKILL.md`, conviene verificar la fuente oficial antes de descartarla.

## Procedencia y fuentes

- Método base: [`pentpest`](https://github.com/AlexaDetalles/pentpest-skill) (MIT), de AlexaDetalles.
- [OWASP Top 10](https://owasp.org/Top10/) (edición 2025).
- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/) (2023).
- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/) (2025).
- [OWASP Mobile Top 10](https://owasp.org/www-project-mobile-top-10/) (2024) y [MASVS](https://mas.owasp.org/MASVS/) 2.1.0.
- [OWASP Top 10 CI/CD Security Risks](https://owasp.org/www-project-top-10-ci-cd-security-risks/).
- [CWE Top 25 Most Dangerous Software Weaknesses](https://cwe.mitre.org/top25/) (CISA/MITRE, edición 2024).
- [OWASP ASVS](https://github.com/OWASP/ASVS) 5.0.
- [MITRE ATT&CK](https://attack.mitre.org/) (matriz Enterprise).
- Guías de buenas prácticas de gestión de API keys/secretos (Stripe, AWS, HashiCorp Vault, MDN Web Security).

Este repositorio es un proyecto independiente, sin afiliación con OWASP, MITRE, CISA ni Anthropic.

## Licencia

MIT. Ver [LICENSE](./LICENSE). El contenido original de `pentpest` conserva su propia licencia MIT; ver [NOTICE.md](./NOTICE.md).
