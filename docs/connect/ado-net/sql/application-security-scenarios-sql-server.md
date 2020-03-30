---
title: SQL Server의 애플리케이션 보안 시나리오
description: ADO.NET 및 SQL Server 애플리케이션에 대한 다양한 애플리케이션 보안 시나리오를 설명하는 항목을 제공합니다.
ms.date: 09/26/2019
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 76ed05f39cba61ea7f26deaef6cd38552b11f199
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897077"
---
# <a name="application-security-scenarios-in-sql-server"></a>SQL Server의 애플리케이션 보안 시나리오

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

보안 SQL Server 클라이언트 애플리케이션을 만드는 한 가지 올바른 방법은 없습니다. 모든 애플리케이션은 요구 사항, 배포 환경 및 사용자 집단에서 고유합니다. 처음 배포될 때 적절하게 보호되는 애플리케이션은 시간이 지남에 따라 보안성이 떨어질 수 있습니다. 향후 발생할 수 있는 위협을 예측할 수는 없습니다.  
  
SQL Server는 제품으로서 개발자가 안전한 데이터베이스 애플리케이션을 만들 수 있는 최신 보안 기능을 통합하기 위해 여러 버전으로 발전했습니다. 그러나 보안은 기본적으로 제공되는 것이 아닙니다. 지속적인 모니터링과 업데이트가 필요합니다.  
  
## <a name="common-threats"></a>일반적인 위협  
개발자는 보안 위협, 이러한 문제를 해결하기 위해 제공된 도구 및 자체의 보안 허점을 방지하는 방법을 이해해야 합니다. 보안은 체인으로 볼 수 있습니다. 한 연결 고리가 끊어지면 전체 강도가 훼손되는 것입니다. 다음 목록에는 이 섹션의 항목에서 자세히 설명하는 몇 가지 일반적인 보안 위협이 나와 있습니다.  
  
### <a name="sql-injection"></a>SQL 인젝션  
SQL 삽입은 악의적인 사용자가 유효한 입력 대신 Transact-SQL 문을 입력하는 프로세스입니다. 입력이 유효성 검사를 거치지 않고 서버로 직접 전달되고 애플리케이션이 삽입된 코드를 실수로 실행하는 경우 공격으로 인해 데이터가 손상되거나 제거될 수 있습니다. 저장 프로시저 및 매개 변수화된 명령을 사용하면 SQL Server 삽입 공격을 차단하여 동적 SQL을 방지하고 모든 사용자에 대해 권한을 제한할 수 있습니다.  
  
### <a name="elevation-of-privilege"></a>권한 상승  
권한 상승 공격은 사용자가 소유자 또는 관리자와 같은 신뢰할 수 있는 계정에 대한 권한을 수임할 수 있는 경우 발생합니다. 항상 최소 권한 사용자 계정에서 실행하고 필요한 권한만 할당합니다. 코드를 실행하는 데 관리자 또는 소유자 계정을 사용하지 마세요. 그러면 공격이 성공할 경우 발생할 수 있는 피해가 제한됩니다. 추가 권한이 필요한 작업을 수행하는 경우 작업 기간 동안만 프로시저 서명 또는 가장을 사용합니다. 때 인증서를 사용하여 저장 프로시저에 서명하거나 임시로 권한을 할당하는 가장을 사용할 수 있습니다.  
  
### <a name="probing-and-intelligent-observation"></a>검색 및 지능적 관찰  
검색 공격은 애플리케이션에서 생성된 오류 메시지를 사용하여 보안 취약성을 검색할 수 있습니다. 모든 프로시저 코드에서 오류 처리를 구현하여 SQL Server 오류 정보가 최종 사용자에게 반환되는 것을 방지합니다.  
  
### <a name="authentication"></a>인증  
사용자 입력을 기반으로 하는 연결 문자열이 런타임에 생성되는 경우 SQL Server 로그인을 사용할 때 연결 문자열 삽입 공격이 발생할 수 있습니다. 유효한 키워드 쌍에 대해 연결 문자열을 확인하지 않으면 공격자가 추가 문자를 삽입하여 서버에서 중요한 데이터 또는 기타 리소스에 액세스할 수 있습니다. 가능하면 Windows 인증을 사용하세요. SQL Server 로그인을 사용해야 하는 경우 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>를 사용하여 런타임에 연결 문자열을 만들고 유효성을 검사합니다.  
  
### <a name="passwords"></a>암호  
침입자가 권한 있는 사용자에 대한 암호를 얻거나 추측할 수 있어 많은 공격이 성공합니다. 암호는 침입을 막는 최전방 방어선이므로 시스템 보안을 위해서는 반드시 강력한 암호를 설정해야 합니다. 혼합 모드 인증에 대한 암호 정책을 만들고 강화합니다.  
  
Windows 인증을 사용하는 경우에도 항상 강력한 암호를 `sa` 계정에 할당합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[SQL Server에서 보안 동적 SQL 작성](writing-secure-dynamic-sql.md)  
저장 프로시저를 사용하여 보안 동적 SQL을 작성하는 기술에 대해 설명합니다.  

## <a name="next-steps"></a>다음 단계
- [SQL Server 보안](sql-server-security.md)
