# Glossary

Each term below has one meaning everywhere in the Helios estate: in every repository's
specifications, documents and code comments. Each entry gives that meaning and, where it helps,
what the term is not.

## The board, its people and its programs

- **caller**: anyone or anything connected to one of the board's listeners for callers, signed in
  or not. Not a user, which is a signed-in person without the Sysop role.
- **engine**: `hadv-service`, the board's server program; its own subsystems are the ones compiled
  into it, not custom scripts.
- **local log**: the server's own record of the engine's events, one line per event, each line
  one key and its value (`key=value`), written to standard output. Not the central audit system; a bare "log" means both.
- **log**: an entry in both the server's local log and the central audit system, unless a line
  names one.
- **server**: one computer, physical or virtual, running the board.
- **sysop**: anyone holding the Sysop role, the default role that runs the board.
- **user**: a person who uses the board without the Sysop role.

## Callers and connections

- **greeting**: the first text the engine writes to a caller after negotiation. Not a login
  screen.
- **kind of connection**: one way a caller reaches the board, such as Telnet or SSH: its
  listeners, how it opens a connection (Telnet's negotiation, SSH's handshake) and its own close,
  behind the same calls for every kind. Not a listener, which is one address and port.
- **listener**: one address and port at which the engine accepts callers. Not a caller, and not
  the engine.
- **negotiation**: the exchange of option requests between the engine and a caller, from the
  moment the engine accepts the caller until it ends the exchange.
- **opening requests**: the option requests the engine sends first to a new caller, before reading
  anything; in Part 1, WILL ECHO then WILL SGA. Not a reply to a request.
- **option request**: a Telnet WILL, WONT, DO or DONT for one Telnet option, sent by either
  side.
- **shared execution path**: the part of the engine that serves every accepted connection the
  same way, whatever its kind of connection: the cap on open connections, the ceiling on a call,
  the session and the close. Not a listener, which only accepts.
- **stop signal**: a signal from the sysop or the operating system that tells the engine to stop.
  Never anything a caller sends.
- **Telnet option**: an option of the Telnet protocol, such as ECHO or SGA, that either side
  offers or refuses. Not a command-line option or any other kind of option.

## Design

- **layer**: one part of a large outcome, brainstormed into a page of its own, then specified and
  built on its own; `PROCESS.md` in HeliosDesign calls it a slice.
- **oracle**: what the tests check behavior against: an existing implementation, run as a black box
  and never read, or one written for the tests, apart from the code it tests.
- **trust boundary**: where data or control crosses from something less trusted into something
  more trusted: network input reaching the engine, a user's action reaching sysop powers, the
  board's own process calling the operating system as an administrator. Guards belong at these,
  not on every operation. Not an interface boundary (a class's public interface or a function's
  parameters) and not a system boundary (where the board's code calls something that is not its
  own: the operating system, a library, a network service). Always written in full.
