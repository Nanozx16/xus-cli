# xus-cli
Quick Start
Installation
Precompiled Binary (Recommended)
For the simplest and most reliable installation:

curl https://cli.nexus.xyz/ | sh
This will:

Download and install the latest precompiled binary for your platform.
Prompt you to accept the Terms of Use.
Start the CLI in interactive mode.
The exact installation script is viewable here.

Non-Interactive Installation
For automated installations (e.g., in CI):

curl -sSf https://cli.nexus.xyz/ -o install.sh
chmod +x install.sh
NONINTERACTIVE=1 ./install.sh
Proving
Proving with the CLI is documented here.

To start with an existing node ID, run:

nexus-cli start --node-id <your-node-id>
Alternatively, you can register your wallet address and create a node ID with the CLI, or at app.nexus.xyz.

nexus-cli register-user --wallet-address <your-wallet-address>
nexus-cli register-node
nexus-cli start
The register-user and register-node commands will save your credentials to ~/.nexus/config.json. To clear credentials, run:

nexus-cli logout
For troubleshooting or to see available command line options, run:

nexus-cli --help
Use Docker
Make sure docker and docker compose have been installed on you machine. check documentation here:

Install Docker
Install Docker Compose
Then, modify the node id in the docker-compose.yaml file, run:

docker compose build --no-cache
docker compose up -d
Check log

docker compose logs
If you want to shut down, run:

docker compose down
Terms of Use
Use of the CLI is subject to the Terms of Use. First-time users running interactively will be prompted to accept these terms.

Node ID
During the CLI's startup, you'll be asked for your node ID. To skip prompts in a non-interactive environment, manually create a ~/.nexus/config.json in the following format:

{
   "node_id": "<YOUR NODE ID>"
}
Current Limitations
To submit programs to the network for proving, contact growth@nexus.xyz.
Get Help
Network FAQ
Discord Community
Technical issues? Open an issue
Contributing
Interested in contributing to the Nexus Network CLI? Check out our Contributor Guide for:

Development setup instructions
How to report issues and submit pull requests
Our code of conduct and community guidelines
Tips for working with the codebase
For most users, we recommend using the precompiled binaries as described above. The contributor guide is intended for those who want to modify or improve the CLI itself.

🛠 Developer Guide
The following steps may be required in order to setup a development environment for contributing to the project:

Linux
sudo apt update
sudo apt upgrade
sudo apt install build-essential pkg-config libssl-dev git-all
sudo apt install protobuf-compiler
macOS
# Install using Homebrew
brew install protobuf

# Verify installation
protoc --version
Windows
Install WSL, then see Linux instructions above.

# Install using Chocolatey
choco install protobuf
Building ProtoBuf files
To build the ProtoBuf files, run the following command in the clients/cli directory:

cargo build --features build_proto
Creating a Release
To create a release, update the package version in Cargo.toml, then create and push a new (annotated) tag, e.g.:

git tag -a v0.1.2 -m "Release v0.1.2"
git push origin v0.1.2
This will trigger the GitHub Actions release workflow that compiles binaries and pushes the Docker image, in addition to creating release.

WARNING: Creating a release through the GitHub UI creates a new release but does NOT trigger the workflow. This leads to a release without a Docker image or binaries, which breaks the installation script.
