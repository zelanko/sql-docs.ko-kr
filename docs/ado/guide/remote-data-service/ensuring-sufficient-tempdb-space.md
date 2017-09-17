---
title: "충분 한 TempDB 공간 확인 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32f05f84953b09f4d727fe6bcba7b4230825faa2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ensuring-sufficient-tempdb-space"></a>충분 한 TempDB 공간 확인
처리 하는 동안 오류가 발생 하면 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 를 Microsoft SQL Server 6.5에서 공간을 처리 해야 하는 개체는 TempDB의 크기가 증가 해야 할 수 있습니다. (임시 처리 공간을 필요로 하는 일부 쿼리에; ORDER BY 절을 사용 하 여 쿼리 정렬 해야 하는 예를 들어의 **레코드 집합**, 일부 임시 공간이 필요 합니다.)  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
> [!IMPORTANT]
>  확장 되는 장치를 축소 하는 것이 쉽지 때문에 작업을 수행 하기 전에이 절차를 자세히 읽습니다.  
  
> [!NOTE]
>  기본 inMicrosoft으로 SQL Server 7.0 이상, TempDB는 필요에 따라 자동 증가 하도록 설정 됩니다. 따라서이 절차 7.0 이전 버전을 실행 하는 서버에 수만 있습니다.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>SQL Server 6.5의 TempDB 공간을 늘리려면  
  
1.  Microsoft SQL Server 엔터프라이즈 관리자를 시작, 트리는 서버에 대 한 연 다음 데이터베이스 장치 트리를 엽니다.  
  
2.  마스터를 확장 하려면 (실제) 장치를 선택 하 고 열려는 장치를 두 번의 **데이터베이스 장치 편집** 대화 상자.  
  
     이 대화 상자에서는 현재 데이터베이스를 사용 하는 공간의 양을 보여 줍니다.  
  
3.  에 **크기** 상자을 원하는 시간 (예를 들어 50 메가바이트 (MB)의 하드 디스크 공간) 장치를 늘립니다.  
  
4.  클릭 **변경 이제** (논리적) TempDB 확장할 수 있는 공간의 크기를 증가 합니다.  
  
5.  서버에서 데이터베이스 트리를 열고 다음 두 번 클릭 **TempDB** 열려는 **데이터베이스 편집** 대화 상자. **데이터베이스** 탭 TempDB에 현재 할당 된 공간의 크기를 보여 줍니다 (**데이터 크기**). 기본적으로 2MB입니다.  
  
6.  아래는 **크기** 그룹에서 클릭 **확장**합니다. 그래프의 각 물리적 장치에 사용 가능 하 고 할당 된 공간을 표시합니다. 적갈색 색에서 막대 사용 가능한 공간을 나타냅니다.  
  
7.  선택 된 **로그 장치**, 마스터에 사용할 수 있는 크기를 표시 하는 **크기 (MB)** 상자.  
  
8.  클릭 **이제 확장** TempDB 데이터베이스에 해당 공간을 할당 합니다.  
  
     **데이터베이스 편집** 대화 상자 표시 새 TempDB에 대 한 할당 크기입니다.  
  
 이 항목에 대 한 자세한 내용은 "확장 데이터베이스 대화 상자"에 대 한 Microsoft SQL Server 엔터프라이즈 관리자 도움말 파일을 검색  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)



