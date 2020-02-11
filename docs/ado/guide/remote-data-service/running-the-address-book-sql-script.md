---
title: 주소록 SQL 스크립트 실행 | Microsoft Docs
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
ms.openlocfilehash: 5adc631a3c3f7a66c02f9ebfe541fa5e923deb0a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922236"
---
# <a name="running-the-address-book-sql-script"></a>주소록 SQL 스크립트 실행
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 다음과 같은 Sampleemp를 SQL Server Enterprise 사용 하 여 포함 된 SQL 스크립트 ()를 실행 해야 합니다.  
  
-   기본 장치에 새 데이터베이스 AddrBookDB를 만듭니다.  
  
-   AddrBookDB 데이터베이스에 연결 합니다.  
  
-   Employee 테이블을 만듭니다.  
  
-   예제 데이터로 테이블을 채웁니다.  
  
-   간단한 SELECT 문을 실행 하 여 데이터베이스 테이블의 채우기를 확인 합니다.  
  
-   암호 "adcdemo"를 사용 하 여 "adcdemo" 라는 사용자 계정을 설정 합니다.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5에서 Sampleemp 스크립트를 실행 하려면  
  
1.  **시작**을 클릭 하 고 **프로그램**을 가리킨 다음 **Microsoft SQL Server 6.5**를 가리킵니다. **SQL 엔터프라이즈 관리자**를 클릭 합니다.  
  
2.  **도구** 메뉴에서 **SQL 쿼리 도구**를 클릭 합니다.  
  
3.  **SQL 스크립트 로드** 를 클릭 하 고 C:\platform SDK\Samples\DataAccess\RDS\AddressBook.로 이동 합니다.  
  
4.  Sampleemp 파일을 선택 합니다. **열기**를 클릭합니다.  
  
5.  **쿼리 실행** 단추 (도구 모음에서 녹색 화살표)를 클릭 합니다.  
  
6.  실행 한 후 **쿼리** 및 **엔터프라이즈 관리자** 창을 닫습니다.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0에서 Sampleemp 스크립트를 실행 하려면  
  
1.  **시작**을 클릭 하 고 **프로그램**을 가리킨 다음 **Microsoft SQL Server 7.0**를 가리킵니다. **엔터프라이즈 관리자**를 클릭 합니다.  
  
2.  엔터프라이즈 관리자의 등록 된 서버 목록에서 사용 하려는 SQL Server를 선택 해야 합니다.  
  
3.  **도구** 메뉴에서 **SQL Server 쿼리 분석기**를 클릭 합니다.  
  
4.  **SQL 스크립트 로드** 단추 (도구 모음에서 폴더 열기)를 클릭 하 고 C:\platform SDK\Samples\DataAccess\RDS\AddressBook.로 이동 합니다.  
  
5.  Sampleemp 파일을 선택 합니다. **열기**를 클릭합니다.  
  
6.  **쿼리 실행** 단추 (도구 모음에서 녹색 화살표) 또는 **F5 키**를 누릅니다.  
  
7.  실행 한 후 **쿼리**, **쿼리 분석기**및 **엔터프라이즈 관리자** 창을 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [주소록 예제 애플리케이션 실행](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


