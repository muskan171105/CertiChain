# Blockchain-Based Digital Certification Platform

A decentralized platform for issuing, verifying, and managing digital certificates using the Ethereum blockchain. The platform ensures certificate immutability, transparency, and easy verification while providing a secure, decentralized solution for storing certificate data using IPFS.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Smart Contract Details](#smart-contract-details)
- [Project Setup](#project-setup)
- [Usage](#usage)
- [File Structure](#file-structure)
- [License](#license)

## Overview

This platform allows institutions to issue digital certificates that can be verified by any third party. The certificates are stored on the Ethereum blockchain, making them tamper-proof and easily accessible for verification. IPFS is used to store large certificate files, ensuring decentralization and data integrity.

### Key Components:

1. **Smart Contracts**: Used for issuing and verifying certificates on the Ethereum blockchain.
2. **IPFS**: Decentralized file storage for certificate files.
3. **React Frontend**: User-friendly interface for institutions and verifiers.
4. **Flask Backend**: API for managing user data and certificate issuance.
5. **MetaMask Integration**: For wallet management and signing blockchain transactions.

## Features

- **Certificate Issuance**: Institutions can issue certificates, which are stored on the blockchain.
- **Verification**: Third parties can verify certificates using the unique certificate ID.
- **Decentralized Storage**: Certificate files are stored on IPFS, with their hash saved on the blockchain.
- **Immutable Records**: Once issued, certificates cannot be altered or tampered with.
- **Secure Wallet Authentication**: Institutions sign transactions through MetaMask for secure issuance.

## Tech Stack

- **Ethereum**: Blockchain network for smart contracts.
- **Solidity**: Smart contract development language.
- **IPFS**: Decentralized storage for certificate files.
- **React**: Frontend framework.
- **Web3.js**: Ethereum interaction in the frontend.
- **Flask**: Backend API.
- **PostgreSQL**: Database for storing user information.
- **MetaMask**: Wallet integration for Ethereum transactions.

## Smart Contract Details

The smart contracts are written in Solidity and include functionality for:

- **Issuing Certificates**: Storing certificate details and the IPFS hash on-chain.
- **Verifying Certificates**: Retrieving certificate details using the certificate ID.
- **Revoking Certificates**: Allowing institutions to revoke a certificate if necessary.

```solidity
pragma solidity ^0.8.0;

contract CertificateRegistry {
    struct Certificate {
        string studentName;
        string institution;
        string course;
        string ipfsHash;
        uint256 issueDate;
    }

    mapping(bytes32 => Certificate) public certificates;

    function issueCertificate(
        string memory studentName, 
        string memory institution, 
        string memory course, 
        string memory ipfsHash
    ) public {
        bytes32 certificateId = keccak256(abi.encodePacked(studentName, institution, course));
        certificates[certificateId] = Certificate(studentName, institution, course, ipfsHash, block.timestamp);
    }

    function verifyCertificate(bytes32 certificateId) public view returns (Certificate memory) {
        return certificates[certificateId];
    }
}
## File Structure

```bash
blockchain-certification-platform/
│
├── blockchain/        # Ethereum smart contracts and Truffle setup
├── client/            # React frontend code
├── backend/           # Flask backend for API and database management
│
├── README.md          # Project documentation
├── .gitignore         # Files to ignore in the repository
└── package.json       # Dependencies and scripts for the frontend
