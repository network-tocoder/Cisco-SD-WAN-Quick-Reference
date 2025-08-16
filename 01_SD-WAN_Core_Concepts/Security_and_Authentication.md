## Security & Authentication

### PKI Certificates
- **Controllers**: vBond, vSmart, and vManage use PKI certificates for authentication
- **Encryption**: All control & management-plane traffic sent over DTLS is AES-256 encrypted
- **Data Traffic**: Actual user traffic uses IPSec encryption

### Transport Protocol
- **Base Port**: UDP port 12346
- **NAT Traversal**: Can hop around ports for NAT compatibility
