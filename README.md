# Go gRPC Project

This project is a gRPC-based application written in Go. It provides services for managing categories and courses, with a SQLite database as the backend.

## Project Structure

```
.
├── cmd/
│   └── grpcServer/
│       └── main.go           # Entry point for the gRPC server
├── internal/
│   ├── database/
│   │   ├── category.go       # Database logic for categories
│   │   └── course.go         # Database logic for courses
│   ├── pb/
│   │   ├── course_category.pb.go       # Generated protobuf code
│   │   └── course_category_grpc.pb.go # Generated gRPC code
│   └── service/
│       └── category.go       # gRPC service implementation for categories
├── proto/
│   └── course_category.proto # Protobuf definitions
├── db.sqlite                 # SQLite database file
├── go.mod                    # Go module file
├── go.sum                    # Go dependencies
└── README.md                 # Project documentation
```

## Prerequisites

- Go 1.24.2 or later
- `protoc` (Protocol Buffers compiler)
- `protoc-gen-go` and `protoc-gen-go-grpc` plugins
- SQLite3

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/angelo848/go-grpc.git
   cd go-grpc
   ```

2. Install dependencies:
   ```bash
   go mod tidy
   ```

3. Generate protobuf and gRPC code:
   ```bash
   protoc --go_out=. --go-grpc_out=. proto/course_category.proto
   ```

4. Run the gRPC server:
   ```bash
   go run cmd/grpcServer/main.go
   ```

## Usage

The gRPC server listens on port `50051`. You can interact with it using a gRPC client. The following services are available:

- **CategoryService**
  - `CreateCategory`: Create a new category.
  - `ListCategories`: List all categories.
  - `GetCategory`: Get details of a specific category.
  - `CreateCategoryStream`: Stream multiple category creation requests.
  - `CreateCategoryStreamBidirectional`: Bidirectional streaming for category creation.

## Database

The project uses a SQLite database (`db.sqlite`) to store categories and courses. Ensure the database file exists and has the required schema before running the server.

## Testing with a gRPC client

Any gRPC client can connect with this server, I used [evans](https://github.com/ktr0731/evans) client for testing these gRPC services.

Example usage:
1. `evans -r repl`: Enter the evans REPL mode
2. `package pb`: Select the **pb** package where the services are located
3. `service CategoryService`: Select the CategoryService
4. `call <rpc_service>` (e.g.: `call ListCategories` )`: Call the desired rpc

https://github.com/user-attachments/assets/ec29666c-b5b9-4abb-b796-29a80c55a488

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
