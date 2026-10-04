# Glossary

Each term below has one meaning everywhere in the Helios estate: in every repository's
specifications, documents and code comments. Each entry gives that meaning and, where it helps,
what the term is not.

## The board, its people and its programs

- **#1 Sysop**: the main Sysop, the #1 account, who owns the board.
- **admin sign-in**: signing in to the Admin API, by anyone holding the permission for it; by default
  only the Sysop role holds it. Not a paired server's certificate.
- **Admin API**: the sysops' endpoint on each server, on its own port. Not the ClusterAPI.
- **alert**: a message that reaches every sysop directly; how it travels is the central audit
  system's. Not a log entry and not an event.
- **ClusterAPI**: the servers' endpoint on each server, on its own port, open only to paired
  servers. Not the Admin API.
- **configuration utilities**: `hadv-config` and `hadv-config-gui`. Not `hadv-setup`, which runs
  only on the server itself.
- **custom script**: a Lua script a sysop adds; not part of the engine.
- **database connection**: where and how a server reaches the database: its address, port and
  connection settings. Not the server's database account.
- **detailed health report**: the Admin API's report on a server's state, which needs a sign-in. Not
  health status.
- **door**: a door game, an external program the board runs for a caller; used in no other sense.
- **engine**: `hadv-service`, the board's server program; its own subsystems are the ones compiled
  into it, not custom scripts.
- **engine release**: one released version of the engine; servers run at most one release apart.
  Not a format version or a vault-key version.
- **event subsystem**: the multi-server-aware subsystem that carries events between subsystems and
  decides when an event runs and on which server, so the same event never runs on two servers; it
  tells the responsible subsystem to do the work and never owns it. Not an alert.
- **`hadv-setup`**: the setup wizard; it runs only on the server itself. **First setup** is its path
  that seeds the first server; **restore** rebuilds a server from a backup and the recovery code.
  Not the configuration utilities.
- **health status**: what a registered server's public, basic health check answers: whether it is
  running and reachable. Not the Admin API's detailed health report, which needs a sign-in.
- **helper program**: one of the board's own programs running beside the engine on the same server
  and doing part of the board's ongoing work (the mail processors, `hadv-xyz`, `hadv-doors`); it
  receives only the secrets it owns, if any. `hadv-setup` and the configuration utilities are not
  helper programs.
- **import utility**: the CLI/TUI tool that brings files into an area through the Admin API.
- **joining**: `hadv-setup`'s path that adds a server to a board that already has one. **joining
  again**: joining for a server that lost its bootstrap file, after server deletion removes its old
  registration. Not restore, which is for a one-server board.
- **log**: an entry in both the server's local log and the central audit system, unless a line
  names one.
- **message system**: the engine subsystem for message areas and mail.
- **network-mail subsystem**: the engine subsystem that exchanges mail with other systems: FidoNet
  technology networks, WWIVnet technology networks, QWK and EQWK networks, VirtualNET technology
  networks, NNTP technology networks, and Internet email.
- **NOTIFY**: PostgreSQL's NOTIFY, a nudge to listening servers; it never carries a key or a
  secret. Not an alert.
- **paired server**: a server that has joined the board and holds the certificate joining gave it.
  Not a registered server, which is known by its public keys.
- **program folder**: the folder holding the board's installed programs, which updates and
  uninstalls touch and a container image rebuilds. Not the bootstrap folder or a work folder.
- **registered server**: a server whose two public keys are registered in the database and which
  has not been deleted. Not a paired server, and not a server that is running (its health status).
- **server**: one computer, physical or virtual, running the board.
- **server deletion**: removing a server from the board through the configuration utilities.
- **service registration**: the OS's record that runs `hadv-service` as a service (the systemd unit,
  or the Windows service's command line), written by `hadv-setup`, changeable only by root or
  administrators. Not a registered server.
- **session password**: the password two FidoNet-technology nodes share for a link.
- **sysop**: anyone holding the Sysop role, who runs the board. **Sysop role**: the default role
  that runs the board.
- **user**: a person who uses the board without the Sysop role.

## Storage

- **area**: a file area or a message area, as storage sees it: the files of one kind kept under one
  folder, or one disc path, on one registry entry. Not a registry entry.
- **available**: none of missing, damaged, unreachable, unavailable or full.
- **damaged**: its hash differs from the recorded hash.
- **drive-letter administrative share**: a share named by one letter followed by `$` (`C$`).
- **file area**: an area of files offered for download.
- **full**: too little room for the write.
- **hidden**: on a storage, seen only by the owning subsystem. **visible**: appears in listings and
  can be opened.
- **identity**: what tells one thing apart from the others of its kind: for a secret, the name its
  owner gives it, unique for that owner; for a registry entry, the value its marker file holds.
- **kind**: a category of files registered by an engine subsystem (file areas, message
  attachments), with its own folder on each writable registry entry.
- **limit**: the most space the board may use on a registry entry; optional, set by the sysop.
- **low-space warning level**: the room below which the sysop is warned.
- **marker file**: a small file at a writable registry entry's path holding that entry's identity.
- **missing**: in the records, but not on its storage.
- **Name**: an area's short identifier: no spaces, stored uppercase, unique within its kind; on a
  writable registry entry, the area's folder name. Not the descriptions users see.
- **owning subsystem**: the engine subsystem that asked the storage subsystem to keep a file, and
  decides who may use it. Not the owner of a secret.
- **path rules**: where a registry entry may point: no root path, nothing inside a refused location,
  no drive-letter administrative share or `ADMIN$`, no entry inside another or containing another.
- **refused-characters list**: the characters and names unsafe on any supported OS; not settled
  yet.
- **refused-locations list**: the system folders per OS, the board's program folders and the
  database's data folder; the system folders are not settled yet.
- **registry entry**: the record describing one storage: its kind, path, owning server and
  credentials. **the registry**: the list of all registry entries.
- **room**: the limit minus the space used, and on local and SMB registry entries no more than the
  storage's free space.
- **root path**: the top of a drive or file system (`C:\`, `/`).
- **scrub job**: a job that reads every file on a registry entry and compares its hash.
- **size limits**: the bounds the storage subsystem sets on every size an SMB server or an ISO image
  states; not settled yet.
- **storage**: a physical place where the board's files live: a folder on a server's disk, an SMB
  share, an S3 bucket, an ISO or an optical drive. Not the database.
- **storage subsystem**: the part of the engine that reaches storages and does the broad checks.
- **unavailable**: found, but not what it should be, so it is not used: a storage that answers but
  is not the one its registry entry describes, or an image that is malformed; a stored value that
  fails to decrypt. Not missing (not there at all) and not unreachable (cannot be contacted).
- **unreachable**: the storage cannot be contacted.
- **volume label and serial**: the name and number recorded on a disc or image when it was made.
- **work folder**: a server's own local folder for files in progress and optical copies, outside
  the registry.

## Shared secrets

- **authenticated helper program**: a helper program that has proven which helper it is on the
  channel that delivers its secrets.
- **bootstrap file**: the per-server file holding the database connection, the server's database
  account, the vault key and the server's private keys. Not the shared vault.
- **bootstrap folder**: the folder, owned by the service account, that holds the bootstrap file,
  separate from the program folder. Not the database's data folder.
- **bootstrap key**: the random 256-bit key a server's bootstrap file is sealed under, held only by
  that server's OS credential store (or, by the sysop's explicit choice, a key file). Not the vault
  key.
- **bootstrap key subsystem**: the per-server subsystem that keeps the bootstrap file sealed under
  the bootstrap key, has the OS credential store seal that key, and unlocks the file for
  `hadv-setup` and `hadv-service`. Not the shared secrets subsystem.
- **build** / **rewrite** (a bootstrap file): to build is for `hadv-setup` to make a new bootstrap
  file, at first setup, joining, joining again or restore; to rewrite is to replace the existing file
  with a changed one, written beside it and swapped in, by `hadv-setup` or `hadv-service`.
- **copy** (of the vault key): the vault key encrypted to one server's or the recovery key's public
  key, and signed. Used in no other sense: never a clipboard copy.
- **envelope**: what surrounds the bootstrap file's named fields: the format version, the sealing and
  the layout. Not the fields themselves.
- **format version**: recorded on every value, every copy of the vault key and the head of every
  bootstrap file: which layout, cipher and derivation it uses. **vault-key version**: recorded on
  every value: which vault key encrypted it. Neither is the engine release.
- **half-made file**: a new bootstrap file a rewrite left beside the old one without swapping it in.
  Not a corrupt bootstrap file.
- **host key**: systemd's per-machine credential key, kept on the server's disk, under which systemd
  credentials seal the bootstrap key, alone or with the TPM. Not an SSH host key.
- **integrity check**: the part of sealing that detects any change to the bootstrap file, its
  unencrypted format version included.
- **key file**: a file the sysop makes, holding the bootstrap key as base64, used only where no OS
  credential store fits and only by the sysop's explicit choice. The bootstrap key in it is not
  sealed.
- **looser than its rule**: open to an account the rule does not name, or giving an account more than
  the rule allows.
- **machine key pair**: the non-exportable Windows key pair made for one server, under which the OS
  credential store seals the bootstrap key. Not a server's receiving, signing or recovery key pair.
- **not set**, **refused**: the read results besides a value and unavailable: no value stored; the
  reader is not the secret's owner.
- **OS credential store**: the store that seals a server's bootstrap key: the CNG key store on
  Windows, systemd credentials on Linux, a Swarm secret in a container. Not the key file.
- **OS software key store**: Windows' key store kept in software, holding the machine key pair where
  there is no TPM. Not the OS credential store as a whole.
- **owner**: the engine subsystem or helper program a secret belongs to, named when it is stored;
  the only one that reads it, or, for a helper program, the only one it is delivered to. Not the
  owning subsystem of a stored file.
- **receiving key pair**, **signing key pair**: a server's two single-purpose key pairs; one opens
  the copies sent to it, the other signs the copies it makes. Neither is the server's TLS
  certificate.
- **recovery code**: the 24 numbered words that rebuild the recovery key pair. Not a backup
  password.
- **recovery copy**: the copy of the vault key made for the recovery key. Not a backup.
- **recovery key pair**: the key pair whose private half the recovery code rebuilds.
- **seal** / **unseal**: to encrypt with authenticated encryption, so that the thing is hidden and
  any change to it is detected; to unseal is to decrypt it and check it. Said of a value, a key or
  a file, always naming what it is sealed under or by.
- **secret**: one owner's named entry in the shared vault: its owner, identity and value. Not a
  "shared secret" in the protocol sense; that is a session password.
- **service account**: the dedicated low-privilege OS account `hadv-service` runs under. Not a
  database account.
- **shared secrets subsystem**: the part of the engine that keeps the secrets every server needs,
  encrypted in the shared vault, and hands each only to its owner.
- **shared vault**: the shared secrets subsystem's store, in the database, holding the secrets every
  server shares (registry entries' credentials, network node passwords and the like). Not the
  bootstrap file.
- **store**, **read**, **delete**, **status**, **deliver**: the five operations on secrets, and
  nothing more. "Store" is never the OS credential store; "deliver" is only ever to a helper
  program.
- **unlock** (the bootstrap): unseal the bootstrap key from the OS credential store (or read it from
  the key file), then unseal the file under it.
- **value**: the opaque bytes a secret holds, which the vault never interprets. Not a setting's
  value in the configuration.
- **vault key**: the one key every server keeps in its bootstrap file; each value's working key is
  derived from it; never stored in the database.
- **vault-key change**: replacing the vault key and re-encrypting every value under the new one.
- **vault-key fields**: the bootstrap file's fields that hold the vault key, the old and the new one
  during a vault-key change; the only fields `hadv-service` changes. Not the vault-key version.
- **vault-key schedule**: the yearly vault-key change, on by default, settable from 45 days to two
  years, switched off only by the #1 Sysop. Not the event subsystem's schedule as a whole.
- **working key**: the key that encrypts one write of one value, derived from the vault key, owner,
  identity and salt.
