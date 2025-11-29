
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/*
 * @title Disease Outbreak Alert DAOs
 * @dev A decentralized platform for reporting, verifying, and alerting disease outbreaks
 * using blockchain for transparency and immutability.
 */

contract DiseaseOutbreakAlertDAO {
    // --- Data Structures ---
    struct Outbreak {
        uint id;
        string diseaseName;
        string location;
        uint256 dateReported;
        address reporter;
        bool verified;
    }

    uint public outbreakCount;
    mapping(uint => Outbreak) public outbreaks;
    address public admin;

    // --- Events ---
    event OutbreakReported(uint id, string diseaseName, string location, address reporter);
    event OutbreakVerified(uint id, string diseaseName, string location, address verifier);

    // --- Constructor ---
    constructor() {
        admin = msg.sender;
    }

    // --- Core Functions ---

    /// @notice Report a new disease outbreak
    function reportOutbreak(string memory _diseaseName, string memory _location) public {
        outbreakCount++;
        outbreaks[outbreakCount] = Outbreak(
            outbreakCount,
            _diseaseName,
            _location,
            block.timestamp,
            msg.sender,
            false
        );
        emit OutbreakReported(outbreakCount, _diseaseName, _location, msg.sender);
    }

    /// @notice Verify a reported outbreak (admin only)
    function verifyOutbreak(uint _id) public {
        require(msg.sender == admin, "Only admin can verify outbreaks");
        require(_id > 0 && _id <= outbreakCount, "Invalid outbreak ID");
        outbreaks[_id].verified = true;
        emit OutbreakVerified(_id, outbreaks[_id].diseaseName, outbreaks[_id].location, msg.sender);
    }

    /// @notice Get details of a specific outbreak
    function getOutbreak(uint _id) public view returns (
        string memory diseaseName,
        string memory location,
        uint256 dateReported,
        address reporter,
        bool verified
    ) {
        require(_id > 0 && _id <= outbreakCount, "Invalid outbreak ID");
        Outbreak memory o = outbreaks[_id];
        return (o.diseaseName, o.location, o.dateReported, o.reporter, o.verified);
    }
}
