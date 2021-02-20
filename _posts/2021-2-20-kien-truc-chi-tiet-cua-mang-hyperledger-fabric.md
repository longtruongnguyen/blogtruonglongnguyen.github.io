---
layout: post
title: Kiến trúc chi tiết của mạng Hyperledger Fabric
description:
excerpt:
thumbnail: 
keywords: mạng Hyperledger Fabric, blockchain, smart contract, chaincode, Membership Service Provider, peer, ledger, Hyperledger
author: Nguyễn Trường Long
---

### Giới thiệu về mạng Hyperledger Fabric

### Mô hình Hyperledger Fabric

- <i>Assets</i>: Có thể hiểu asset trong mạng Hyperledger Fabric được định nghĩa là mọi thứ có giá trị bao gồm tài sản hữu hình và tài sản vô hình (hợp đồng và tài sản trí tuệ). Hyperledger Fabric cung cấp khả năng sửa đổi tài sản bằng cách sử dụng các chaincode transaction.

### Các thành phần của mạng Hyperledger Fabric

- Ledger: Một ledger (sổ cái) bao gồm 2 phần khác nhau là "blockchain" và "state database".
- Membership Service Provider: Membership Service Provider (MSP) là một thành phần của hệ thống có nhiệm vụ cung cấp các chứng chỉ (credential) cho client và peer để họ tham gia vào Hyperledger Fabric network.
- Smart Contract: Smart Contract là một đoạn mã được gọi bởi ứng dụng của client bên ngoài mạng blockchain - quản lý quyền truy cập và sửa đổi đối với một tập hợp các cặp khóa-giá trị ở "state database".
- Peer: Peer là thành phần cơ bản của network, được sở hữu và duy trì bởi các thành viên. Đây là nơi lưu trữ các bản sao của ledger và các bản sao của smart contract. Trong ví dụ sau, mạng N bao gồm các peer node là P1, P2 và P3. Mỗi peer node này đều chứa bản sảo của sổ cái phân tán (distributed ledger) L1. P1, P2 và P3 đều sử dụng chung chaincode S1 để truy cập vào bản sao sổ cái phân tán của nó. Các peer node có thể được tạo, dừng, cấu hình lại và xóa. Có một tập hợp các API cho phép các quản trị viên và ứng dụng tương tác với services mà họ cung cấp.
- Mạng Fabric thực hiện smart contract với công nghệ có tên gọi là chaincode. Có thể hiểu đơn giản chaincode là một đoạn code được dùng để truy cập vào sổ cái. Chaincode được viết dưới dạng một ngôn ngữ lập trình.
