# Changelog

## v5.0.0 2021-12-27

- `amqplib-as-promised/lib` now exports wrapped (Promise-based) `ConfirmChannel` instead of the amqplib's native one.
- Updated vulnerable dependencies.

## v4.0.0 2019-12-02

- Support channel with confirmation mode.
- Methods `publish` and `sendToChannel` for standard mode resolve to `unknown`
  type and `Replies.Empty` for confirmation mode.

## v3.15.3 2019-10-10

- Updated dependencies.
- Uses `mocha-steps` for testing.
