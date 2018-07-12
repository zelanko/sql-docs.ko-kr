---
title: 'Isqlservererrorinfo:: Geterrorinfo (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f33c66d8e521339573e56b78407f0bab67b4b43e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430102"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo(OLE DB)
  에 대 한 포인터를 반환 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 SSERRORINFO 구조를 포함 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 세부 정보입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
   HRESULT GetErrorInfo(  
SSERRORINFO**ppSSErrorInfo,  
OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>인수  
 *ppSSErrorInfo*[out]  
 SSERRORINFO 구조에 대한 포인터입니다. 메서드가 실패 하거나 하는 경우 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류와 관련 된 정보를 공급자 메모리를 할당 하지 않습니다 하 고 있는지 확인 합니다 *ppSSErrorInfo* 인수는 출력에 null 포인터입니다.  
  
 *ppErrorStrings*[out]  
 유니코드 문자열 포인터에 대한 포인터입니다. 메서드가 실패 하거나 하는 경우 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 오류와 관련 된 정보 공급자 메모리를 할당 하지 않습니다 및 되도록 합니다 *ppErrorStrings* 인수는 출력에 null 포인터입니다. 해제 합니다 *ppErrorStrings* 인수를 합니다 **imalloc:: Free** 메서드는 메모리 블록에서 할당 되는 대로의 반환 된 SSERRORINFO 구조에 세 명의 개별 문자열 멤버를 해제 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_INVALIDARG  
 중 하나는 *ppSSErrorInfo* 또는 *ppErrorStrings* 인수가 NULL입니다.  
  
 E_OUTOFMEMORY  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 요청을 완료할 충분 한 메모리를 할당 하지 못했습니다.  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 전달 된 포인터를 통해 반환 된 SSERRORINFO 및 OLECHAR 문자열에 대 한 메모리를 할당 합니다. 소비자를 사용 하 여이 메모리를 할당 취소 해야 합니다 **imalloc:: Free** 메서드는 오류 데이터에 대 한 액세스를 더 이상 필요 합니다.  
  
 SSERRORINFO 구조는 다음과 같이 정의됩니다.  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|멤버|Description|  
|------------|-----------------|  
|*pwszMessage*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전달하는 오류 메시지입니다. 메시지를 통해 반환 되는 **ierrorinfo:: Getdescription** 메서드.|  
|*pwszServer*|오류가 발생한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|*pwszProcedure*|오류가 저장 프로시저에서 발생한 경우에는 오류를 생성한 저장 프로시저의 이름이고, 그렇지 않으면 빈 문자열입니다.|  
|*lNative*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 번호입니다. 오류 번호는 반환 되는 동일 합니다 *과 같습니다* 의 매개 변수를 **isqlerrorinfo:: Getsqlinfo** 메서드.|  
|*bState*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류의 상태입니다.|  
|*bClass*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류의 심각도입니다.|  
|*wLineNumber*|해당되는 경우 오류 메시지가 발생한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저의 줄입니다. 저장 프로시저가 연관되지 않은 경우 기본값은 1입니다.|  
  
 반환 된 문자열의 주소를 참조 하는 구조에 대 한 포인터를 *ppErrorStrings* 인수입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)   
 [RAISERROR&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
