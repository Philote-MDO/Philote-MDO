# Implicit Disciplines

    service ImplicitService {
        // Calls the discipline Compute function
        rpc ComputeResiduals(stream Array) returns (stream Array) {}

        // Calls the discipline RPC that solves the nonlinear equations
        rpc SolveResiduals(stream Array) returns (stream Array) {}

        // Calls the discipline ComputePartials function
        rpc ComputeResidualGradients(stream Array) returns (stream Array) {}
    }