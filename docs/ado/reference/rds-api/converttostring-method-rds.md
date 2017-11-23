---
title: "ConvertToString 메서드 (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd7be0ef5fae5bd05dfa5f7c1a31b98341f30117
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="converttostring-method-rds"></a>ConvertToString 메서드 (RDS)
변환 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) MIME 나타내는 문자열을 레코드 집합 데이터를 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataFactory*  
 개체 변수를 나타내는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체입니다.  
  
 *레코드 집합*  
 개체 변수를 나타내는 **레코드 집합** 개체입니다.  
  
## <a name="remarks"></a>주의  
 .Asp 파일을 사용 하 여 **ConvertToString** 포함 하는 **레코드 집합** 클라이언트 컴퓨터에 전송 하는 서버에서 생성 된 HTML 페이지에 있습니다.  
  
 **ConvertToString** 이 처음 로드는 **레코드 집합** 커서 서비스에 테이블을 선택한 다음 스트림을 MIME 형식으로 생성 합니다.  
  
 클라이언트에서 원격 데이터 서비스 수 MIME 문자열으로 다시 변환할 완전 하 게 작동 **레코드 집합**합니다. 보다 적은 400 행당 1024 바이트 너비까지 데이터 행을 처리 하는 데 작동 합니다. BLOB 데이터를 스트리밍에 사용해 서는 안 및 HTTP를 통해 큰 결과 집합입니다. 실시간 압축 하지 않고 매우 큰 데이터 집합을 정의 하 고 해당 기본 전송 프로토콜 형식으로 원격 데이터 서비스에서 배포한 유선 액세스에 최적화 된 테이블 그램 형식 비교 했을 때 HTTP를 통해 전송 시간이 오래 걸릴 됩니다는 문자열에서 수행 됩니다.  
  
> [!NOTE]
>  Active Server Pages 클라이언트 HTML 페이지에 결과 MIME 문자열을 포함 하려면를 사용 하는 경우에 버전 2.0 보다 이전 버전의 VBScript 문자열의 크기는 32k를 제한 하는 주의 해야 합니다. 이 제한을 초과 하는 경우 오류가 반환 됩니다. MIME.asp 파일을 통해 포함을 사용할 때 쿼리 범위를 상대적으로 작게 유지 합니다. 이 해결 하려면 Microsoft Windows 스크립트 기술을 웹 사이트에서 VBScript의 최신 버전을 다운로드 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ConvertToString 메서드 예제 (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 메서드 예제(VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


