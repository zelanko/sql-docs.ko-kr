---
title: 주소록 SQL 스크립트를 실행 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 366e1a5812b4d8152e5c8965d3059e3a6b2ca1cb
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704199"
---
# <a name="running-the-address-book-sql-script"></a>주소록 SQL 스크립트 실행
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 ISQL/쿼리 분석기 명령줄 유틸리티 또는 SQL Server 엔터프라이즈 관리자를 사용 해야 합니다 (Sampleemp.sql) 포함 된 SQL 스크립트를 실행 합니다.  
  
-   기본 장치에 AddrBookDB, 새 데이터베이스를 만듭니다.  
  
-   AddrBookDB 데이터베이스에 연결합니다.  
  
-   직원 테이블을 만듭니다.  
  
-   샘플 데이터로 테이블을 채웁니다.  
  
-   데이터베이스 테이블의 채우기를 확인 하는 간단한 SELECT 문을 실행 합니다.  
  
-   "Adcdemo." 암호를 사용 하 여 "adcdemo" 이라는 사용자 계정을 설정 합니다.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5에서 Sampleemp.sql 스크립트를 실행 하려면  
  
1.  클릭 **시작**, 가리킨 **프로그램**를 가리킨 다음 **Microsoft SQL Server 6.5**합니다. 클릭 **SQL 엔터프라이즈 관리자**합니다.  
  
2.  **도구** 메뉴에서 클릭 **SQL 쿼리 도구**합니다.  
  
3.  클릭 **SQL 스크립트 로드** c:\Platform SDK\Samples\DataAccess\RDS\AddressBook 찾습니다.  
  
4.  Sampleemp.sql 파일을 선택 합니다. **열기**를 클릭합니다.  
  
5.  클릭 합니다 **쿼리 실행** 단추 (도구 모음에서 녹색 화살표).  
  
6.  를 실행 한 후 닫습니다 합니다 **쿼리** 하 고 **엔터프라이즈 관리자** windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0에서 Sampleemp.sql 스크립트를 실행 하려면  
  
1.  클릭 **시작**, 가리킨 **프로그램**를 가리킨 다음 **Microsoft SQL Server 7.0**합니다. 클릭 **엔터프라이즈 관리자**합니다.  
  
2.  사용 하려는 SQL Server Enterprise Manager에서 등록 된 서버 목록에서 선택 되어 있는지 확인 해야 합니다.  
  
3.  **도구** 메뉴에서 클릭 **SQL Server 쿼리 분석기**합니다.  
  
4.  클릭 합니다 **SQL 스크립트 로드** c:\Platform SDK\Samples\DataAccess\RDS\AddressBook 찾아 단추 (도구 모음에서 열린 폴더).  
  
5.  Sampleemp.sql 파일을 선택 합니다. **열기**를 클릭합니다.  
  
6.  클릭 합니다 **쿼리 실행** (도구 모음에서 녹색 화살표) 단추 또는 **F5**합니다.  
  
7.  를 실행 한 후 닫습니다 합니다 **쿼리**를 **쿼리 분석기**, 및 **엔터프라이즈 관리자** windows.  
  
## <a name="see-also"></a>관련 항목  
 [주소록 예제 응용 프로그램 실행](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


