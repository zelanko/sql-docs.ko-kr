---
title: IBCPSession2::BCPSetBulkMode | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BCPSetBulkMode function
ms.assetid: babba19f-e67b-450c-b0e6-523a0f9d23ab
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b0cd923904b13e9cb63b72010e89d4079b966e22
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39539183"
---
# <a name="ibcpsession2bcpsetbulkmode"></a>IBCPSession2::BCPSetBulkMode
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  IBCPSession2::BCPSetBulkMode 대안을 제공 [ibcpsession:: Bcpcolfmt &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) 열 형식을 지정 합니다. Ibcpsession:: Bcpcolfmt를 개별 열 형식 특성을 설정 하는 달리 IBCPSession2::BCPSetBulkMode 모든 특성을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPSetBulkMode (  
      int property,  
   void * pField,  
   int cbField,  
   void * pRow,  
   int cbRow  
);  
```  
  
## <a name="arguments"></a>인수  
 *property*  
 BYTE 유형의 상수입니다. 상수 목록은 주의 섹션의 표를 참조하십시오.  
  
 *pField*  
 필드 종결자 값에 대한 포인터입니다.  
  
 cbField  
 필드 종결자 값의 길이(바이트)입니다.  
  
 pRow  
 행 종결자 값에 대한 포인터입니다.  
  
 cbRow  
 행 종결자 값의 길이(바이트)입니다.  
  
## <a name="returns"></a>반환 값  
 IBCPSession2::BCPSetBulkMode 다음 중 하나를 반환할 수 있습니다.  
  
|||  
|-|-|  
|**S_OK**|메서드가 성공했습니다.|  
|**E_FAIL**|공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 ISQLServerErrorInfo 인터페이스를 사용하세요.|  
|**E_UNEXPECTED**|예기치 않은 메서드가 호출되었습니다. 예를 들어 합니다 **IBCPSession2::BCPInit** IBCPSession2::BCPSetBulkMode를 호출 하기 전에 메서드가 호출 되지 않았습니다.|  
|**E_INVALIDARG**|잘못된 인수입니다.|  
|**E_OUTOFMEMORY**|메모리 부족 오류가 발생했습니다.|  
  
## <a name="remarks"></a>Remarks  
 IBCPSession2::BCPSetBulkMode 대량 쿼리 또는 테이블에서 복사를 사용할 수 있습니다. 쿼리 문을 대량 복사하는 데 사용되는 IBCPSession2::BCPSetBulkMode는 `IBCPSession::BCPControl(BCP_OPTIONS_HINTS, …)`를 호출하여 쿼리 문을 지정하기 전에 호출해야 합니다.  
  
 단일 명령 텍스트에서 RPC 호출 구문을 일괄 처리 쿼리 구문(예:`{rpc func};SELECT * from Tbl`)과 결합하지 마십시오.  이렇게 하면 오류를 반환 하 고 메타 데이터를 검색할 수 없도록 하려면 icommandprepare:: Prepare 합니다. 단일 명령 텍스트에서 저장 프로시저 실행 및 일괄 처리 쿼리를 결합해야 할 경우 ODBC CALL 구문(예:`{call func}; SELECT * from Tbl`)을 사용합니다.  
  
 다음 표에서는 *property* 매개 변수에 대한 상수를 나열합니다.  
  
|property|Description|  
|--------------|-----------------|  
|BCP_OUT_CHARACTER_MODE|문자 출력 모드를 지정합니다.<br /><br /> BCP의 – c 옵션에 해당합니다. EXE를 사용 하 여 ibcpsession:: Bcpcolfmt *eUserDataType* 속성으로 설정 **BCP_TYPE_SQLCHARACTER**합니다.|  
|BCP_OUT_WIDE_CHARACTER_MODE|유니코드 출력 모드를 지정합니다.<br /><br /> BCP의 – w 옵션에 해당합니다. EXE 및 사용 하 여 ibcpsession:: Bcpcolfmt *eUserDataType* 속성으로 설정 **BCP_TYPE_SQLNCHAR**합니다.|  
|BCP_OUT_NATIVE_TEXT_MODE|비문자 유형의 경우 네이티브 유형을 지정하고 문자 유형의 경우 유니코드를 지정합니다.<br /><br /> BCP의 – N 옵션에 해당합니다. EXE 및 사용 하 여 ibcpsession:: Bcpcolfmt *eUserDataType* 속성으로 설정 **BCP_TYPE_SQLNCHAR** 열 유형이 문자열인 경우 또는 **BCP_TYPE_DEFAULT** 문자열이 아닌 경우.|  
|BCP_OUT_NATIVE_MODE|네이티브 데이터베이스 유형을 지정합니다.<br /><br /> BCP의 – n 옵션에 해당합니다. EXE 및 사용 하 여 ibcpsession:: Bcpcolfmt *eUserDataType* 속성으로 설정 **BCP_TYPE_DEFAULT**합니다.|  
  
 Ibcpsession:: Bcpcontrol 및 IBCPSession2::BCPSetBulkMode IBCPSession2::BCPSetBulkMode와 충돌 하지 않는 ibcpsession:: Bcpcontrol 옵션에 대해 호출할 수 있습니다. 예를 들어 ibcpsession:: Bcpcontrol 사용 하 여 호출할 수 있습니다 **BCP_OPTION_FIRST** 및 IBCPSession2::BCPSetBulkMode 합니다.  
  
 Ibcpsession:: Bcpcontrol 사용 하 여 호출할 수 없습니다 **BCP_OPTION_TEXTFILE** 및 IBCPSession2::BCPSetBulkMode 합니다.  
  
 Ibcpsession:: Bcpcolfmt, ibcpsession:: Bcpcontrol, 및 ibcpsession:: Bcpreadfmt를 포함 하는 함수 호출의 시퀀스를 사용 하 여 IBCPSession2::BCPSetBulkMode를 호출 하려고 하면 함수 호출 중 하나는 시퀀스 오류 실패를 반환 합니다. 이러한 오류를 해결하도록 선택하는 경우 IBCPSession::BCPInit를 호출하여 설정을 재설정하고 다시 시작합니다.  
  
 함수 시퀀스 오류가 발생 하는 함수 호출의 몇 가지 예는 다음과 같습니다.  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_IN);  
BCPSetBulkMode();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPReadFmt();  
```  
  
```  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_HINTS, "select …");  
BCPSetBulkMode();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPColFmt();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPReadFmt();  
BCPColFmt();  
```  
  
```  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetBulkMode();  
BCPControl(BCP_OPTION_HINTS, "select …");  
BCPReadFmt();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPColumns();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetColFmt();  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 IBCPSession2::BCPSetBulkMode의 서로 다른 설정을 사용하여 4개의 파일을 만듭니다.  
  
```  
  
// compile with: sqlncli11.lib oleaut32.lib ole32.lib  
  
#include <stdio.h>  
#include "sqlncli.h"  
  
IDBInitialize*  g_pIDBInitialize = NULL;  
IBCPSession2 * g_pIBcpSession = NULL;  
class COLEDBPropSet : public DBPROPSET {  
public:  
   COLEDBPropSet() {  
      rgProperties = NULL;  
      cProperties = 0;  
   };  
   COLEDBPropSet(const GUID& guid) {  
      rgProperties = NULL;  
      cProperties = 0;  
      guidPropertySet = guid;  
   };  
   ~COLEDBPropSet() {  
      for ( ULONG i = 0 ; i < cProperties ; i++ )  
         VariantClear(&rgProperties[i].vValue);  
      CoTaskMemFree(rgProperties);  
   }  
   void SetGUID(const GUID& guid) {  
      guidPropertySet = guid;  
   };  
   bool AddProperty(DWORD dwPropertyID, bool bValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BOOL;  
      rgProperties[cProperties].vValue.boolVal = (bValue) ? VARIANT_TRUE : VARIANT_FALSE;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID, long nValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID  = dwPropertyID;  
      rgProperties[cProperties].vValue.vt     = VT_I4;  
      rgProperties[cProperties].vValue.lVal   = nValue;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID,LPCWSTR szValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BSTR;  
      rgProperties[cProperties].vValue.bstrVal = SysAllocString(szValue);  
      cProperties++;  
      return true;  
   };  
   bool Add() {  
      DBPROP* p = (DBPROP*)CoTaskMemRealloc(rgProperties, (cProperties + 1) * sizeof(DBPROP));  
      if (p != NULL) {  
         rgProperties = p;  
         rgProperties[cProperties].dwOptions = DBPROPOPTIONS_REQUIRED;  
         rgProperties[cProperties].colid = DB_NULLID;  
         rgProperties[cProperties].vValue.vt = VT_EMPTY;  
         return true;  
      }  
      else  
         return false;  
   };  
};  
  
void OLEDBCleanUp() {  
   if (g_pIDBInitialize) {  
      g_pIDBInitialize->Release();  
      g_pIDBInitialize = NULL;  
   }  
   if (g_pIBcpSession) {  
      g_pIBcpSession->Release();  
      g_pIBcpSession = NULL;  
   }  
}  
  
BOOL MakeOLEDBConnect(LPWSTR  pServer) {  
   BOOL ret = true;  
   IDBProperties * pIDBProperties = NULL;  
   IDBCreateSession * pIDBCreateSession = NULL;  
   COLEDBPropSet PropSet(DBPROPSET_DBINIT);  
   COLEDBPropSet BcpProperty(DBPROPSET_SQLSERVERDATASOURCE);  
   try {  
      HRESULT hr = CoInitializeEx(NULL,COINIT_MULTITHREADED);   
      hr = CoCreateInstance(SQLNCLI_CLSID, NULL, CLSCTX_INPROC_SERVER, IID_IDBInitialize, (LPVOID *)&g_pIDBInitialize);  
      if (FAILED(hr)) {  
         printf("CoCreateInstance failed\n");  
         return false;  
      }  
      PropSet.AddProperty(DBPROP_INIT_DATASOURCE, (LPWSTR)pServer);  
      PropSet.AddProperty(DBPROP_AUTH_INTEGRATED, L"SSPI");  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBProperties, (void**) &pIDBProperties);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->QueryInterface(IID_IDBProperties...) failed\n");  
         throw false;  
      }  
      hr = pIDBProperties->SetProperties(1, &PropSet);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties(...) failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->Initialize();  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->Initialize() failed\n");  
         throw false;  
      }  
      BcpProperty.AddProperty(SSPROP_ENABLEFASTLOAD, true);  
      BcpProperty.AddProperty(SSPROP_ENABLEBULKCOPY, true);  
      hr = pIDBProperties->SetProperties(1, &BcpProperty);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties() for bcp failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBCreateSession, (void**) &pIDBCreateSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->QueryInterface(IID_IDBCreateSession..) failed\n");  
         throw false;  
      }  
  
      hr = pIDBCreateSession->CreateSession(NULL, IID_IBCPSession2, (IUnknown**) &g_pIBcpSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBCreateSession->CreateSession() failed\n");  
         throw false;  
      }  
   }  
   catch(...) {  
      ret = false;  
   }  
   if (pIDBProperties)  
      pIDBProperties->Release();  
   if (pIDBCreateSession)  
      pIDBCreateSession->Release();  
   return ret;  
}  
  
BOOL BCPSetBulkMode(LPWSTR pszServer, LPTSTR pszQureryOut, char BCPType, LPWSTR pszDataFile) {  
   HRESULThr;  
   if (!MakeOLEDBConnect(pszServer))  
      return false;  
   hr = g_pIBcpSession->BCPInit(NULL, pszDataFile, NULL, BCP_DIRECTION_OUT );   // bcp init for queryout  
   if (FAILED(hr)) {  
      printf("BCP init failed\n");  
      OLEDBCleanUp();  
      return false;  
   }  
   // setbulkmode  
   char ColTerm[] = "\t";  
   char RowTerm[] = "\r\n";  
   wchar_t wColTerm[] = L"\t";  
   wchar_t wRowTerm[] = L"\r\n";  
   BYTE * pColTerm = NULL;  
   int cbColTerm = NULL;  
   BYTE * pRowTerm = 0;  
   int cbRowTerm = 0;  
   int bulkmode = -1;  
  
   if(BCPType == 'c') {   // bcp -c  
      pColTerm = (BYTE*)ColTerm;  
      pRowTerm = (BYTE*)RowTerm;  
      cbColTerm = 1;  
      cbRowTerm = 2;  
      bulkmode = BCP_OUT_CHARACTER_MODE;  
   }  
   else  
      if(BCPType == 'w') {   // bcp -w  
         pColTerm = (BYTE*)wColTerm;  
         pRowTerm = (BYTE*)wRowTerm;  
         cbColTerm = 2;  
         cbRowTerm = 4;  
         bulkmode = BCP_OUT_WIDE_CHARACTER_MODE;  
      }  
      else  
         if (BCPType == 'n')   // bcp -n  
            bulkmode = BCP_OUT_NATIVE_MODE;  
         else  
            if (BCPType == 'N')   // bcp -n  
               bulkmode = BCP_OUT_NATIVE_TEXT_MODE;  
            else {  
               printf("unknown bcp mode\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            hr = g_pIBcpSession->BCPSetBulkMode(bulkmode, pColTerm, cbColTerm, pRowTerm, cbRowTerm);  
            if (FAILED(hr)) {  
               printf("BCPSetBulkMode failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
  
            // set queryout TSQL statement  
            hr = g_pIBcpSession->BCPControl(BCP_OPTION_HINTS, pszQureryOut);  
            if (FAILED(hr)) {  
               printf("BCPControl failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            // bcp copy  
            DBROWCOUNT nRowsInserted = 0;  
            hr = g_pIBcpSession->BCPExec(&nRowsInserted);  
            if (FAILED(hr)) {  
               printf("BCPExec failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            printf("bcp done\n");  
            OLEDBCleanUp();  
            return true;  
}  
  
int main() {  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'c', L"bcpc.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'w', L"bcpw.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'n', L"bcpn.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'N', L"bcp_N.dat");  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [IBCPSession2 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession2-ole-db.md)  
  
  
