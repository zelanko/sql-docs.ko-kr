---
title: ConvertToString 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 426fd1fdcd3931981037b346b048de816e8596d0
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600293"
---
# <a name="converttostring-method-rds"></a>ConvertToString 메서드(RDS)
변환 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 레코드 집합 데이터를 나타내는 MIME 문자열로 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataFactory*  
 나타내는 개체 변수를 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체입니다.  
  
 *레코드 집합*  
 나타내는 개체 변수를 **레코드 집합** 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 .Asp 파일과 함께 사용 하 여 **ConvertToString** 포함 하는 **레코드 집합** 클라이언트 컴퓨터에 전송 서버에서 생성 된 HTML 페이지에 있습니다.  
  
 **ConvertToString** 처음 로드 합니다 **레코드 집합** 커서 서비스에 테이블을 선택한 다음 MIME 형식으로 스트림을 생성 합니다.  
  
 클라이언트에서 원격 데이터 서비스 수 MIME 문자열으로 다시 변환할 완전 하 게 작동 **레코드 집합**합니다. 행 당 1024 바이트 너비 보다 더 이상 사용 하 여 데이터의 400 개 미만의 행을 처리 하는 데 작동 합니다. HTTP를 통해 큰 결과 집합와 BLOB 데이터를 스트리밍에 대 한 사용 하지 않아야 합니다. 실시간 압축 하지 않고 문자열에서 매우 큰 데이터 집합 상당한 시간이 걸립니다 전송으로 HTTP 통신에 최적화 된 테이블 그램 형식을 정의 하 고 해당 네이티브 전송 프로토콜 형식으로 원격 데이터 서비스에서 배포할 비교 했을 때를 통해 수행 됩니다.  
  
> [!NOTE]
>  Active Server Pages를 사용 하 여 클라이언트 HTML 페이지에 결과 MIME 문자열을 포함 하는, 하는 경우 버전 2.0 이전 버전의 VBScript 32k 문자열의 크기를 제한 하는 주의 합니다. 이 제한을 초과 하는 경우 오류가 반환 됩니다. MIME.asp 파일을 통해 포함을 사용 하는 경우 쿼리 범위를 상대적으로 작게 유지 합니다. 이 해결 하려면 Microsoft Windows 스크립트 기술 웹 사이트에서 VBScript의 최신 버전을 다운로드 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>관련 항목  
 [ConvertToString 메서드 예제 (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString 메서드 예제(VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


