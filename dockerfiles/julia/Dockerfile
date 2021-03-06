# For the details and usage of this docker script, please refer to:
# * https://github.com/tuna/tunasync-scripts/pull/71
# * https://github.com/tuna/issues/issues/837

# StorageServer.jl is used to set up a *static* storage server for julia packages, it requires at least Julia 1.4
# The details of the storage protocol can be found in https://github.com/JuliaLang/Pkg.jl/issues/1377
FROM julia:1.4
LABEL description="A community maintained docker script to set up julia mirror easily."
LABEL maintainer="Johnny Chen <johnnychen94@hotmail.com>"

RUN apt-get update && \
    apt-get install -y \
        git && \
    rm -rf /var/lib/apt/lists/*

ENV JULIA_DEPOT_PATH="/tmp/julia"
ENV JULIA_STATIC_DIR="/julia/static"
ENV JULIA_CLONES_DIR="/julia/clones"

# StorageServer.jl is an experimental toolkit and it won't be registered in General
# The API is likely to be changed in the future, so we fix the version here for stability consideration
RUN julia -e 'using Pkg; pkg"add https://github.com/johnnychen94/StorageServer.jl#v0.1.0-rc1"'

RUN chown -R 2000 /tmp/julia/

WORKDIR /julia
CMD /bin/bash
