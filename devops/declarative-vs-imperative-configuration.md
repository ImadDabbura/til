- **Declarative configuration** is when the user describes the desired state of
the system. This means the state is well understood and doesn't need to be
executed to be understood.
- **Imperative Configuration** is when the configuration states the steps
  needed to be executed. It wouldn't usually be clear what would be the desired
  state. Also, it's hard to rollback steps.

Most systems, especially distributed systems such as *Kubernetes*, prefer
declarative configuration because the current state of the system can always be
compared with the declared/desired state.
