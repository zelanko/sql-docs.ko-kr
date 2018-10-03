---
title: 릴리스 정보 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: cb599d59a374fc09dbc0009f0288296cc1df9d9d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702072"
---
# <a name="release-notes"></a>릴리스 정보
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Windows 기반 Microsoft ODBC Driver for SQL Server에 대한 릴리스 정보입니다.  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2의 새로운 기능

**추가 기능**:

자세한 내용은 SQL Server 및 Azure SQL Database에 대 한 데이터 분류 참조 [데이터 분류](../data-classification.md)

서버 인코딩 u t F-8에 대 한 지원

[버그 수정](../bug-fixes.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1의 새로운 기능

**추가 기능**:

에 대 한 지원 `SQL_COPT_SS_CEKCACHETTL` 하 고 `SQL_COPT_SS_TRUSTEDCMKPATHS` 연결 특성 (자세한 내용은 참조 하십시오 [ODBC Driver for SQL Server를 사용 하 여 상시 암호화를 사용 하 여](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` 열 암호화 키의 로컬 캐시에 존재 하는 시간을 제어 뿐만 아니라이 플러시 수 있습니다.
- `SQL_COPT_SS_TRUSTEDCMKPATHS` 만 목록을 사용합니다 하 여 지정 된 열 마스터 키의 AE 작업을 제한 하는 응용 프로그램 사용


Azure Active Directory 대화형 인증 지원

[버그 수정](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17의 새로운 기능

**추가 기능**:

BCP API에 대 한 always Encrypted 지원

새 연결 문자열 특성 UseFMTOnly 드라이버를 임시 테이블을 요구 하는 특별 한 경우에서 레거시 메타 데이터를 사용 하면 됩니다.

Azure SQL 관리 되는 인스턴스 (확장 된 비공개 미리 보기)를 지원 합니다. 
> [!NOTE]
> 관리 되는 인스턴스를 사용 하는 경우 몇 가지 차이점이 가지:
> -   FILESTREAM 지원 되지 않습니다. 
> -   로컬 파일 시스템 액세스는 지원 되지 않지만 tracefiles 등을 위해 필요 하지 않습니다. 
> -   로컬에서 UDT를 만들 경로가 지원 되지 않습니다 
> -   Windows 통합 인증이 지원 되지 않습니다. 
> -   DTC는 지원되지 않습니다. 
> -   'sa' 계정 없는 (기본 계정 이라고 'cloudSA')
> -   잘못 된 서버 이름을 반환 하는 TDS 토큰 오류 (0xAA)
> -   데이터베이스 이름에 특수 문자는 지원 되지 않습니다. 
> -   [Dbname1] ALTER DATABASE MODIFY NAME = [dbname2] 지원 되지 않습니다
> -   오류 메시지는 항상 언어에 관계 없이 영어로 표시 됩니다 (Azure와 동일) 설정 
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1의 새로운 기능  
 ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대 한 지원이 추가 되었습니다 [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 하 고 [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) Microsoft SQL Server 2016과 함께 사용 하는 경우.  해당 연결 풀링 키워드/특성에 설명 되어 있습니다 [드라이버 인식 연결 풀링 ODBC Driver for SQL Server에서에서](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)합니다.

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13의 새로운 기능  
 ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Server 용 ODBC Driver 11에서 이전 기능을 포함 하며 Microsoft SQL Server 2016에 대 한 지원이 추가 되었습니다.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11의 새로운 기능  
 SQL Server용 ODBC 드라이버 11에는 SQL Server 2012 Native Client의 ODBC와 함께 제공되는 모든 기능뿐만 아니라 새로운 [기능](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)이 포함되어 있습니다.  
