---
title: 자격 증명(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: d1a5247e5a6260b77ca3ea5349d6620fec9698dc
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032768"
---
# <a name="credentials-database-engine"></a>자격 증명(데이터베이스 엔진)
  자격 증명은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]외부의 리소스에 연결하는 데 필요한 인증 정보(자격 증명)가 포함된 레코드입니다. 이 정보는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 내부적으로 사용됩니다. 대부분의 자격 증명에는 Windows 사용자 이름 및 암호가 들어 있습니다.  
  
 자격 증명에 저장된 정보를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 연결된 사용자가 서버 인스턴스 외부의 리소스에 액세스할 수 있습니다. 외부 리소스가 Windows인 경우 사용자는 자격 증명에서 지정한 Windows 사용자로 인증됩니다. 하나의 자격 증명을 여러 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에 매핑할 수 있지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인은 하나의 자격 증명에만 매핑할 수 있습니다.  
  
 시스템 자격 증명은 자동으로 생성되며 특정 엔드포인트와 연결됩니다. 시스템 자격 증명의 이름은 2개의 해시 기호(##)로 시작됩니다.  
  
 자격 증명에 대 한 자세한 내용은 참조는 [sys.credentials](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) 카탈로그 뷰.  
  
## <a name="related-content"></a>관련 내용  
 [자격 증명을 만듭니다](../authentication-access/create-a-credential.md) [자격 증명 만들기 &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
 [SQL Server 보안 설정](../securing-sql-server.md)  
  
  
