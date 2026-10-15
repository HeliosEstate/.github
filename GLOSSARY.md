# Glossary

Each term below has one meaning everywhere in the Helios estate: in every repository's
specifications, documents and code comments. Each entry gives that meaning and, where it helps,
what the term is not.

## The board, its people and its programs

- **caller**: anyone or anything connected to one of the board's listeners for callers, signed in
  or not. Not a user, which is a signed-in person without the Sysop role.
- **engine**: `hadv-service`, the board's server program; its own subsystems are the ones compiled
  into it, not custom scripts.
- **`hadv-setup`**: the setup wizard; it runs only on the server itself. Not `hadv-config` or
  `hadv-config-gui`.
- **local log**: the server's own record of the engine's events, one `key=value` line each,
  written to standard output. Not the central audit system; a bare "log" means both.
- **log**: an entry in both the server's local log and the central audit system, unless a line
  names one.
- **server**: one computer, physical or virtual, running the board.
- **subsystem**: the one place responsible for a single job, which fits in one sentence without
  "and". It owns that job's data and rules, and the rest of the system reaches it only through a
  small interface. In Go, a package or a few.
- **sysop**: anyone holding the Sysop role, who runs the board. **Sysop role**: the default role
  that runs the board.
- **user**: a person who uses the board without the Sysop role.

## Callers and connections

- **connection flood**: the time from a connection refused over the cap until 10 seconds pass
  with no refusal; the next refusal starts a new one. Not a flood of messages or of chat.
- **connection ID**: the ID the engine gives each accepted connection, to tie together its lines
  in the local log. Not a user's or a session's ID, and never anything the caller sent.
- **forced stop**: a stop caused by a second stop signal or by closing the console window, in
  which the engine closes the open connections at once.
- **greeting**: the first text the engine writes to a caller after negotiation. Not a login
  screen.
- **listener**: one address and port at which the engine accepts callers. Not a caller, and not
  the engine.
- **negotiation**: the exchange of option requests between the engine and a caller, from the
  moment the engine accepts the caller until it ends the exchange.
- **option request**: a Telnet WILL, WONT, DO or DONT for one Telnet option, sent by either
  side.
- **stop signal**: a signal from the sysop or the operating system that tells the engine to stop.
  Never anything a caller sends.
- **Telnet option**: an option of the Telnet protocol, such as ECHO or SGA, that either side
  offers or refuses. Not a command-line option or any other kind of option.

## Design

- **layer**: one part of a large outcome, brainstormed, specified and built on its own, recorded as
  one Part of the outcome's brief.
- **oracle**: what the tests check behavior against: an existing implementation, run as a black box
  and never read, or one written for the tests, apart from the code it tests.
- **trust boundary**: where data or control crosses from something less trusted into something
  more trusted: network input reaching the engine, a user's action reaching sysop powers, the
  board's own process calling the operating system as an administrator. Guards belong at these,
  not on every operation. Not an interface boundary (a class's public interface or a function's
  parameters) and not a system boundary (where the board's code calls something that is not its
  own: the operating system, a library, a network service). Always written in full.
