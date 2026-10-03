# agent-skills
Reusable skills for kagent agents. One folder per skill under skills/.
Each skill folder contains a SKILL.md (frontmatter: name, description) plus supporting files.

| Skill | Purpose |
|---|---|
| ibm-block-csi | IBM Block CSI Driver 1.14.0 docs and workflows |

```
Use in an Agent:
  spec.skills.gitRefs:
    - url: https://github.com/\<you\>/agent-skills.git
      ref: main
      path: skills/<skill-name>
      name: <skill-name>
```
