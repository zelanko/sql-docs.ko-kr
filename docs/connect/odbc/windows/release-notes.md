---
title: 릴리스 정보 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21380decd228d82695c4ca9972852585a4fc3dbc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32858801"
---
# <a name="release-notes"></a>릴리스 정보
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Windows 기반 Microsoft ODBC Driver for SQL Server에 대한 릴리스 정보입니다.  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>새로운 기능에 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows에서

**추가 된 기능**:

에 대 한 지원 `SQL_COPT_SS_CEKCACHETTL` 및 `SQL_COPT_SS_TRUSTEDCMKPATHS` 연결 특성 (자세한 내용은 참조 [ODBC Driver for SQL Server와 상시 암호화를 사용 하 여](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` 열 암호화 키의 로컬 캐시 존재 하는 시간을 제어 뿐만 아니라이 플러시 있도록 허용
- `SQL_COPT_SS_TRUSTEDCMKPATHS` 열 마스터 키의 지정 된 목록에만 사용 하도록 AE 작업을 제한 하면 응용 프로그램


Azure Active Directory 대화형 인증 지원

[버그 수정](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>새로운 기능에 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 에 대 한 ODBC 드라이버 17 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows에서

**추가 된 기능**:

BCP API에 대 한 상시 암호화 지원

새로운 연결 문자열 특성 UseFMTOnly 드라이버를 임시 테이블을 요구 하는 특별 한 경우에서 레거시 메타 데이터를 사용 하면 됩니다.

Azure SQL 관리 되는 인스턴스 (확장 된 비공개 미리 보기)에 대 한 지원. 
> [!NOTE]
> 관리 되는 인스턴스를 사용 하는 경우 몇 가지 차이점이 있습니다.
> -   FILESTREAM 지원 되지 않습니다. 
> -   로컬 파일 시스템 액세스는 지원 되지만 tracefiles 등의 작업에 필요 하지 
> -   로컬에서 UDT를 만들 경로가 지원 되지 않습니다 
> -   Windows 통합 인증이 지원 되지 않습니다. 
> -   DTC 지원 되지 않습니다. 
> -   'sa' 계정 나타나지 않습니다. (기본 계정 라고 'cloudSA')
> -   잘못 된 서버 이름을 반환 하는 TDS 토큰 오류 (0xAA)
> -   데이터베이스 이름에 특수 문자는 지원 되지 않습니다. 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] 지원 되지 않습니다
> -   오류 메시지는 항상 언어에 관계 없이 영어로 표시 됩니다 (Azure와 같음) 설정 
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>새로운 기능에 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows에서  
 에 대 한 ODBC Driver 13.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 에 대 한 지원을 추가 [항상 암호화](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 및 [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) Microsoft SQL Server 2016와 함께 사용 하는 경우.  해당 연결 풀링 키워드/특성에 설명 된 [드라이버 인식 연결 풀링 ODBC Driver for SQL Server에서에서](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)합니다.

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>새로운 기능에 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows에서  
 ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SQL Server 용 ODBC 드라이버 11에서 이전 기능을 포함 하 고 Microsoft SQL Server 2016에 대 한 지원을 추가 합니다.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>새로운 기능에 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows에서  
 ODBC Driver 11 for SQL Server 새 포함 [기능](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md) SQL Server 2012 Native Client의 ODBC와 함께 제공 되는 모든 기능 뿐만 아니라 합니다.  
