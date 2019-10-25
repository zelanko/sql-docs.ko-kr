---
title: SQL Server 보안
description: SQL Server 보안 기능에 대해 간략하게 설명하고 SQL Server를 대상으로 하는 안전한 ADO.NET 애플리케이션을 만드는 시나리오를 제공합니다.
ms.date: 09/26/2019
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: bb9e02743122958cb567e01f5011fc9f8b3481e6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451999"
---
# <a name="sql-server-security"></a>SQL Server 보안

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server에는 보안 데이터베이스 애플리케이션을 만들 수 있도록 지원하는 많은 기능이 있습니다.  
  
데이터 절도나 손상같이 일반적으로 발생하는 보안 문제는 사용 중인 SQL Server 버전에 관계없이 항상 고려해야 할 사항입니다. 데이터 무결성도 보안 문제로 간주 해야 합니다. 데이터가 보호 되지 않는 경우 임시 데이터 조작을 허용 하 고 잘못 된 값을 사용 하 여 실수로 또는 악의적으로 데이터를 수정 하거나 완전히 삭제 하는 것이 쓸모 없게 될 수 있습니다. 또한 기밀 정보의 올바른 저장소와 같이 준수 해야 하는 법적 요구 사항도 많습니다. 일부 개인 데이터를 저장 하는 것은 특정 관할지에 적용 되는 법에 따라 완전히 수보다 많으면 됩니다.  
  
Windows가 버전마다 다른 것처럼 SQL Server도 버전마다 보안 기능이 다르며 최신 버전이 이전 버전보다 향상된 보안 기능을 가지고 있습니다. 보안 기능 만으로는 보안 데이터베이스 응용 프로그램을 보장할 수 없다는 것을 이해 하는 것이 중요 합니다. 각 데이터베이스 응용 프로그램은 요구 사항, 실행 환경, 배포 모델, 물리적 위치 및 사용자 집단에서 고유 합니다. 범위에 로컬인 일부 응용 프로그램의 경우 최소한의 보안만 필요할 수 있는 반면, 인터넷을 통해 배포 된 다른 로컬 응용 프로그램이 나 응용 프로그램은 엄격한 보안 조치와 지속적인 모니터링 및 평가를 요구할 수 있습니다.  
  
SQL Server 데이터베이스 애플리케이션의 보안 요구 사항은 디자인 타임부터 고려해야 하며 뒤늦게 생각해서는 안 됩니다. 개발 주기 초기에 위협을 평가 하면 취약성이 발견 될 때마다 잠재적 피해를 완화할 수 있습니다.  
  
응용 프로그램의 초기 디자인이 소리나 더라도 시스템이 진화 함에 따라 새로운 위협이 발생할 수 있습니다. 데이터베이스에 대 한 여러 줄의 방어를 만들어 보안 위반으로 인 한 피해를 최소화할 수 있습니다. 첫 번째 방어선은 절대적으로 필요한 권한 이상의 권한을 부여 하지 않고 공격 노출 영역을 줄이는 것입니다.  
  
이 단원의 항목에서는 개발자와 관련이 있는 SQL Server의 보안 기능에 대해 간략히 설명하며, 이러한 항목에 대해 자세히 다루고 있는 SQL Server 온라인 설명서와 기타 리소스의 관련 항목으로 연결되는 링크를 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[SQL Server에서 인증](authentication-sql-server.md)  
SQL Server의 로그인 및 인증에 대해 설명 하 고 추가 리소스에 대 한 링크를 제공 합니다. 
  
[SQL Server의 애플리케이션 보안 시나리오](application-security-scenarios-sql-server.md)  
ADO.NET 및 SQL Server 애플리케이션에 대한 다양한 애플리케이션 보안 시나리오를 설명하는 항목을 제공합니다.  
  
[SQL Server Express 보안](sql-server-express-security.md)  
SQL Server Express의 보안 고려 사항에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
[SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
SQL Server 및 Azure SQL Database에 대 한 보안 고려 사항을 설명 합니다.

[SQL Server 설치에 대한 보안 고려 사항](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
SQL Server를 설치 하기 전에 고려해 야 하는 보안 문제에 대해 설명 합니다.

## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
