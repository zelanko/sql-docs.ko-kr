---
title: DB2 용 SSMA 클라이언트 설치 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/07/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1623430eed752db7fa387caf33124082eb318490
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70774181"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>DB2 용 SSMA 클라이언트 설치 (DB2ToSQL)

SSMA 클라이언트는 다음 작업을 수행 하는 프로그램 파일로 구성 됩니다.  
  
- DB2 데이터베이스에 연결합니다.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
- DB2 데이터베이스 개체를 구문 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 으로 변환 합니다.  
  
- 개체를에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로드 합니다.  
  
- 데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션합니다.  
  
이 항목에서는 SSMA 설치를 위한 필수 구성 요소 및 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>전제 조건

SSMA는 z/OS 버전 9.0 및 10.0 또는 DB2 (LUW 버전 9.8 및 10.1 이상 버전) 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 이상 버전에서 db2를 사용 하도록 설계 되었습니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
- Windows 7 이상 버전 또는 Windows Server 2008 이상 버전  
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]3.1 이상 버전을 Windows Installer 합니다.  
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 미디어에서 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0을 사용할 수 있습니다. [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수도 있습니다.  
  
- Microsoft OLEDB Provider for DB2 버전 5 이상 버전 및 마이그레이션할 DB2 데이터베이스에 대 한 연결입니다.  
  
- 데이터베이스 개체와 데이터를 마이그레이션할 대상 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB를 호스트 하는 컴퓨터에 대 한 액세스 권한이 있어야 합니다. 자세한 내용은 [SQL Server &#40;DB2eToSQL&#41;에 연결 ](../../ssma/db2/connecting-to-sql-server-db2etosql.md)을 참조 하세요.  
  
- 4gb RAM 권장.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLE DB Provider for DB2  

OLEDB provider for DB2 버전 6.0을 다운로드 하려면 [Microsoft® SQL Server® 2017 기능 팩](https://www.microsoft.com/download/details.aspx?id=55992)으로 이동 합니다.

SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmafordb2)를 참조 하세요.  
  
최신 버전을 다운로드 한 후에 설치 파일의 압축을 풀어 SSMA를 설치할 수 있습니다.  
  
SSMA 클라이언트를 설치 하려면:
  
1. SSMA for DB2 *n*을 두 번 클릭 합니다. Setup.exe를 설치 합니다. 여기서 *n* 은 빌드 번호입니다.  
  
2. **Welcome** 페이지에서 **다음**을 선택합니다.  
  
   필수 구성 요소를 설치 하지 않은 경우 먼저 필수 구성 요소를 설치 해야 한다는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 했는지 확인 한 후 설치 프로그램을 다시 실행 합니다.  
  
3. 최종 사용자 사용권 계약을 읽습니다. 동의 하면 동의 함을 **선택 하**고 **다음**을 선택 합니다.  
  
4. **설치 유형 선택** 페이지에서 **일반**을 선택 합니다.  
  
5. **설치**를 선택합니다.  
  
> [!IMPORTANT]  
> 새 버전을 설치 하기 전에 d b 2 용 SSMA의 모든 이전 버전을 제거 하세요.
  
기본 설치 위치는 d b 2의 경우 C:\Program Files\Microsoft SQL Server Migration Assistant입니다.  
  
## <a name="see-also"></a>참고 항목

[SQL Server &#40;DB2ToSQL&#41;에 SSMA 구성 요소 설치](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[DB2 데이터베이스를 SQL Server &#40;DB2ToSQL&#41;로 마이그레이션](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
