# Echo Ark

A simple WASI example that echoes back the input message with NEAR context information.

## What it does

This example demonstrates how to:
- Read JSON input from stdin
- Access NEAR environment variables (`NEAR_SENDER_ID`, `NEAR_BLOCK_HEIGHT`)
- Output formatted JSON response

## Input Format

```json
{
  "message": "Hello, NEAR!"
}
```

## Output Format

```json
{
  "echo": "user.near said \"Hello, NEAR!\" at block 123456789"
}
```

## Building

```bash
cargo build --target wasm32-wasip1 --release
```

The compiled WASM will be at: `target/wasm32-wasip1/release/echo-ark.wasm`

## Testing Locally

```bash
# Run tests
cargo test

# Test with echo
echo '{"message":"Hello, NEAR!"}' | cargo run
```

## Using with NEAR Offshore

Deploy and call via the dashboard:
1. Push this code to GitHub
2. In the dashboard, set:
   - **Repository**: `https://github.com/your-username/your-repo`
   - **Commit**: `main` (or specific commit hash)
   - **Build Target**: `wasm32-wasip1`
   - **Response Format**: `Json`
   - **Input Data**: `{"message":"Hello from the blockchain!"}`

The contract will receive a parsed JSON response:
```json
{
  "echo": "alice.near said \"Hello from the blockchain!\" at block 123456789"
}
```

## Environment Variables

The following NEAR environment variables are available:
- `NEAR_SENDER_ID` - Account that requested the execution
- `NEAR_BLOCK_HEIGHT` - Block height when the request was made
- `NEAR_BLOCK_TIMESTAMP` - Block timestamp (nanoseconds)
- `NEAR_CONTRACT_ID` - OffchainVM contract address
- `NEAR_REQUEST_ID` - Unique request ID
- `NEAR_MAX_INSTRUCTIONS` - Instruction limit for this execution
- `NEAR_MAX_MEMORY_MB` - Memory limit in MB
- `NEAR_MAX_EXECUTION_SECONDS` - Time limit in seconds
