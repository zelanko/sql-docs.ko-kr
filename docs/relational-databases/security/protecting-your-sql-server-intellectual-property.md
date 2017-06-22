---
title: "SQL Server 지적 재산 보호 | Microsoft 문서"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- protecting intellectual property
- intellectual property
ms.assetid: 174a646a-d65c-4074-8249-d783e91be2dd
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 64297656b09d9f0843127887b490cef98d07b835
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="protecting-your-sql-server-intellectual-property"></a>SQL Server 지적 재산 보호
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

소프트웨어 개발자는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터 응용 프로그램을 고객에게 배포하는 방법을 자주 질문하지만 고객이 직접 응용 프로그램을 분석하고 분해할 수 없도록 합니다. 여기에서 중요한 점은 지적 재산권 보호는 법적 문제이며 이러한 보호는 사용권 계약을 기반으로 한다는 점입니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]가 다른 사람이 관리하는 컴퓨터에 설치되어 있으면 기본적으로 일부 측면을 제어할 수 없습니다. 

## <a name="nature-of-the-problem"></a>문제의 특성
컴퓨터의 소유자/관리자는 해당 컴퓨터에 설치되어 있는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 인스턴스에 항상 액세스할 수 있습니다. 응용 프로그램을 고객의 컴퓨터에 배포하는 경우 관리자이므로 **sysadmin** 고정 서버 역할의 멤버로 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에 연결할 수 있습니다. 여기에는 사용 권한 부여, 백업 관리(다른 컴퓨터로 백업 복원 포함), 데이터 파일 암호 해독 및 이동 등의 기능이 포함됩니다. 자세한 내용은 [시스템 관리자가 잠겨 있는 경우 SQL Server에 연결](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)을 참조하세요. 

저장 프로시저 및 데이터는 암호화할 수 있지만 데이터 구조는 숨길 수 없으며 서버 프로세스에 디버거를 연결할 수 있는 사용자는 런타임에 메모리에서 암호 해독된 프로시저 및 데이터를 검색할 수 있습니다.

클라이언트가 컴퓨터에서 관리자가 아닌 경우 클라이언트의 액세스를 방지할 수 있습니다. You can use [투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption-tde.md)를 사용하여 데이터 파일을 암호화할 수 있으며 백업을 암호화하고 모든 사용자의 작업을 감사할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 관리자 및 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터의 관리자는 이러한 작업을 되돌릴 수 있습니다.

## <a name="solution"></a>해결 방법
클라이언트 컴퓨터에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 설치하지 않고도 다양한 방법으로 클라이언트 데이터 액세스를 구성할 수 있습니다. 가장 쉬운 방법은 [상시 암호화](../../relational-databases/security/encryption/always-encrypted-database-engine.md)와 함께 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]를 사용하여 클라이언트가 관리자가 되지 않도록 하는 것입니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]시작에 대한 자세한 내용은 [SQL Database 정의 SQL Database 소개](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)를 참조하세요.  

또한 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 자신의 네트워크에서 호스트하고 클라이언트가 네트워크를 통해 직접적으로나 웹 응용 프로그램을 통해 데이터에 액세스하도록 할 수 있습니다.

## <a name="see-also"></a>관련 항목:

[SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[SQL Server 보안 설정](../../relational-databases/security/securing-sql-server.md)  


