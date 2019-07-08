---
title: 자격 증명(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 06/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2221eedc3e8a64959183c637493e2b45dfec22ee
ms.sourcegitcommit: ab867100949e932f29d25a3c41171f01156e923d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67419175"
---
# <a name="credentials-database-engine"></a>자격 증명(데이터베이스 엔진)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  자격 증명은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]외부의 리소스에 연결하는 데 필요한 인증 정보(자격 증명)가 포함된 레코드입니다. 이 정보는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 내부적으로 사용됩니다. 대부분의 자격 증명에는 Windows 사용자 이름 및 암호가 들어 있습니다.  
  
 자격 증명에 저장된 정보를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 연결된 사용자가 서버 인스턴스 외부의 리소스에 액세스할 수 있습니다. 외부 리소스가 Windows인 경우 사용자는 자격 증명에서 지정한 Windows 사용자로 인증됩니다. 각 자격 증명을 하나의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에만 매핑할 수 있습니다. 또한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 하나의 자격 증명에만 매핑할 수 있습니다.  
  
 master 데이터베이스에 저장되고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스를 통해 사용할 수 있는 자격 증명은 [CREATE CREDENTIAL&#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)을 참조하세요. 특정 데이터베이스에 사용되고 해당 데이터베이스로 이식 가능한 자격 증명은 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.  
  
 시스템 자격 증명은 자동으로 생성되며 특정 엔드포인트와 연결됩니다. 시스템 자격 증명의 이름은 2개의 해시 기호(##)로 시작됩니다.  
  
 자격 증명에 대한 자세한 내용은 [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) 및 [sys.database_scoped_credentials](../../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 카탈로그 뷰를 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 [자격 증명 만들기](../../../relational-databases/security/authentication-access/create-a-credential.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
 [SQL Server 보안 설정](../../../relational-databases/security/securing-sql-server.md)  
  
  
