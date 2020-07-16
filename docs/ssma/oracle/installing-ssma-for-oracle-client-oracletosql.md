---
title: Oracle 용 SSMA 클라이언트 설치 (OracleToSQL) | Microsoft Docs
description: Oracle 클라이언트용 SSMA (SQL Server Migration Assistant)의 설치 필수 구성 요소 및 설치 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 939504092ef7ae9dc13bdcf829f6ea5e88ce59f9
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411274"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Oracle 용 SSMA 클라이언트 설치 (OracleToSQL)

SSMA 클라이언트는 다음 작업을 수행 하는 프로그램 파일로 구성 됩니다.  
  
- Oracle 데이터베이스에 연결합니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.
- Oracle 데이터베이스 개체를 구문으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.
- 개체를에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.
- 데이터를로 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

이 항목에서는 SSMA 설치를 위한 필수 구성 요소 및 지침을 제공 합니다.

## <a name="prerequisites"></a>필수 조건

SSMA는 Oracle 9 이상 버전 및의 모든 버전에서 작동 하도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.

- Windows 7 이상 버전 또는 Windows Server 2008 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.7.2 이상 버전입니다. [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수 있습니다.
- 마이그레이션하려는 Oracle 데이터베이스에 대 한 연결입니다.
- 대상 인스턴스를 호스트 하는 컴퓨터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 데이터베이스 개체와 데이터를 마이그레이션할 컴퓨터에 대 한 액세스 권한이 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 있어야 합니다. 자세한 내용은 [SQL Server &#40;OracleToSQL&#41;에 연결 ](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)을 참조 하세요.
- 4gb RAM 권장.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Oracle 용 SSMA 클라이언트 설치

SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmafororacle)를 참조 하세요.

SSMA 클라이언트를 설치 하려면:

1. **SSMAforOracle_*n*.msi**를 두 번 클릭 합니다. 여기서 *n* 은 빌드 번호입니다.
2. Welcome 페이지에서 **다음**을 클릭합니다.

   필수 구성 요소가 설치 되어 있지 않은 경우 먼저 필수 구성 요소를 설치 해야 함을 나타내는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 했는지 확인 한 후 설치 프로그램을 다시 실행 합니다.  

3. 최종 사용자 사용권 계약을 읽습니다. 동의 하면 동의 함을 **선택 하**고 **다음**을 클릭 합니다.
4. **설치 유형 선택** 페이지에서 **일반**을 클릭 합니다.
5. **설치 준비 완료** 페이지에서 도구를 시작할 때마다 원격 분석 및 자동 업데이트 검사를 사용 하거나 사용 하지 않도록 설정할 수 있습니다. **설치**를 클릭하여 설치를 시작합니다.

> [!IMPORTANT]
> 새 버전을 설치 하기 전에 Oracle 용 SSMA의 모든 이전 버전을 제거 하세요.

기본 설치 위치는 `C:\Program Files\Microsoft SQL Server Migration Assistant for Oracle`입니다.

SSMA 프로그램 파일 외에도 Oracle 용 SSMA 확장 팩을 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [SQL Server에 SSMA 구성 요소 설치](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)를 참조 하세요.

## <a name="see-also"></a>추가 정보

- [SQL Server에 SSMA 구성 요소 설치](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)
- [Oracle 데이터베이스를 SQL Server로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
