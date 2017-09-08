---
title: "SQL Server의 기계 학습에 대 한 보안 고려 사항 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b5fba856cc40c11f218faf0a61f66ee5451aa4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>SQL Server의 기계 학습에 대 한 보안 고려 사항

이 문서에서는 관리자 또는 설계자 명심 해야 컴퓨터 학습 서비스를 사용 하는 경우 보안 고려 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="use-a-firewall-to-restrict-network-access-by-r"></a>방화벽을 사용 하 여 r의 네트워크 액세스 제한

기본 설치에서 Windows 방화벽 규칙을 사용 하 여 R 런타임 프로세스에서 모든 아웃 바운드 네트워크 액세스를 차단 하 합니다. R 런타임 프로세스가 패키지를 다운로드하거나 악의적일 수 있는 기타 네트워크 호출을 수행하지 못하도록 하려면 방화벽 규칙을 만들어야 합니다.

다른 방화벽 프로그램을 사용하는 경우에는 로컬 사용자 계정 또는 사용자 계정 풀이 나타내는 그룹에 대해 규칙을 설정하여 R 런타임에 대해 아웃바운드 네트워크 연결을 차단할 수도 있습니다.

Python 또는 R 런타임에 아무 제한 없이 네트워크 액세스를 방지 하기 위해 Windows 방화벽 (또는 원하는 다른 방화벽)에서 설정 하는 것이 좋습니다.

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>원격 계산 컨텍스트를 지 원하는 인증 방법

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]Windows 통합 인증 및 SQL 로그인 간의 연결을 만들 때 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 원격 데이터 과학 클라이언트입니다.

예를 들어 랩톱에서 R 솔루션을 개발 중이고 SQL Server 컴퓨터에서 계산을 수행하려면 **rx** 함수를 사용하고 Windows 자격 증명을 기반으로 연결 문자열을 정의하여 R에서 SQL Server 데이터 원본을 만듭니다.

변경 될 때는 _계산 컨텍스트_ 랩톱에 SQL Server 컴퓨터에서 Windows 계정에 필요한 권한이 있으면 모든 R 코드는 실행 SQL Server 컴퓨터에 있습니다. 또한, R 코드의 일부로 실행 되는 모든 SQL 쿼리도 자격 증명에서 실행 됩니다.

SQL 로그인을 사용 하는 SQL Server 인스턴스가 혼합된 모드 인증을 허용 하도록 구성 되어야이 시나리오 에서도 지원 됩니다.

### <a name="implied-authentication"></a>암시적 인증

 일반적으로 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 외부 스크립트 런타임을 시작 하 고는 자체 계정에서 스크립트를 실행 합니다. 그러나, 외부 런타임은 ODBC 호출을 수행 하는 경우는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] ODBC 호출 발생 하지 않도록 하는 명령을 전송 하는 사용자의 자격 증명을 가장 합니다. 이를 *암시적 인증*이라고 합니다.
 
 > [!IMPORTANT]
 >
 > 암시적 인증이 성공하려면 작업자 계정(기본적으로 **SQLRUser**)이 포함된 Windows 사용자 그룹에는 인스턴스에 대한 마스터 데이터베이스의 계정이 있어야 하고 이 계정에는 인스턴스에 연결할 권한이 부여되어야 합니다.
 > 
 > 그룹 **SQLRUser** Python 스크립트를 실행 하는 경우에 사용 됩니다. 

## <a name="no-support-for-encryption-at-rest"></a>휴지 암호화 지원 되지 않음

외부 스크립트 런타임에서 주고 받는 데이터에 대 한 투명 한 데이터 암호화 지원 되지 않습니다. 휴지 암호화는 미사용 **않습니다** 디스크 또는 지속형된 중간 결과를 저장 하는 모든 데이터가 Python 또는 R 스크립트에서 사용 하는 모든 데이터에 적용할 수 있습니다.

## <a name="resources"></a>리소스

R 스크립트를 실행 하는 데 사용 하 여 사용자 계정을 프로 비전 하는 방법에 대 한 서비스를 관리 하는 방법에 대 한 자세한 내용은 참조 [구성 및 고급 분석 확장 관리](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)합니다.

보안 아키텍처에 대 한 참조.

+ [R에 대 한 보안 개요](security-overview-sql-server-r.md)
+ [Python에 대 한 보안 개요](../python/security-overview-sql-server-python-services.md)
