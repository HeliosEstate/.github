# Glossary

Each term below has one meaning everywhere in the Helios estate: in every repository's
specifications, documents and code comments. Each entry gives that meaning and, where it helps,
what the term is not.

## The board, its people and its programs

- **engine**: `hadv-service`, the board's server program; its own subsystems are the ones compiled
  into it, not custom scripts.
- **`hadv-setup`**: the setup wizard; it runs only on the server itself. Not `hadv-config` or
  `hadv-config-gui`.
- **log**: an entry in both the server's local log and the central audit system, unless a line
  names one.
- **server**: one computer, physical or virtual, running the board.
- **subsystem**: the one place responsible for a single job, which fits in one sentence without
  "and". It owns that job's data and rules, and the rest of the system reaches it only through a
  small interface. In Go, a package or a few.
- **sysop**: anyone holding the Sysop role, who runs the board. **Sysop role**: the default role
  that runs the board.
- **user**: a person who uses the board without the Sysop role.

## Design

- **trust boundary**: where data or control crosses from something less trusted into something
  more trusted: network input reaching the engine, a user's action reaching sysop powers, the
  board's own process calling the operating system as an administrator. Guards belong at these,
  not on every operation. Not an interface boundary (a class's public interface or a function's
  parameters) and not a system boundary (where the board's code calls something that is not its
  own: the operating system, a library, a network service). Always written in full.
