#ifndef VAKSIN_H_INCLUDED
#define VAKSIN_H_INCLUDED

#include <iostream>
using namespace std;

#define next(P) P->next
#define prev(P) P->prev
#define first(L) L.first
#define last(L) L.last
#define info(P) P->info

typedef string infotype_v;
typedef struct elmist_vaksin *addr_vaksin;

struct elmist_vaksin{
    infotype_v info;
    addr_vaksin next;
    addr_vaksin prev;
};

struct List_vaksin {
    addr_vaksin first;
    addr_vaksin last;
};
addr_vaksin alokasi(infotype_v x);
addr_vaksin findElm_Vaksin(List_vaksin L, infotype_v P);

void createListVaksin(List_vaksin &L);

void insertFirstVaksin(List_vaksin &L, addr_vaksin P);
void insertLastVaksin(List_vaksin &L, addr_vaksin P);

void deleteFirst_Vaksin(List_vaksin &L, addr_vaksin &P);
void deleteLast_Vaksin(List_vaksin &L, addr_vaksin &P);
void deleteAfter_Vaksin(List_vaksin &L,addr_vaksin &P, addr_vaksin Q);

void printVaksin(List_vaksin &L);

void SearchInfoVaksin(List_vaksin L,addr_vaksin Q);

#endif // VAKSIN_H_INCLUDED


#include "vaksin.h"

void createListVaksin(List_vaksin &L){
    first(L) = NULL;
    last(L) = NULL;
}

addr_vaksin alokasi(infotype_v x){
    addr_vaksin P = new elmist_vaksin;
    info(P) = x;
    next(P) = NULL;
    prev(P) = NULL;

    return P;
}



void insertFirstVaksin(List_vaksin &L, addr_vaksin P){
    if(first(L) == NULL){
        first(L) = P;
        last(L) = P;
        prev(P) = NULL;
    }else{
        prev(first(L))=P;
        next(P) = first(L);
        first(L) = P;
    }
}
void insertLastVaksin(List_vaksin &L, addr_vaksin P){
    if(first(L) == NULL){
        insertFirstVaksin(L,P);
    }else{
        next(last(L)) = P;
        prev(P) = last(L);
        last(L) = P;
    }
}

addr_vaksin findElm_Vaksin(List_vaksin L, infotype_v x){
    addr_vaksin P = first(L);
    while(P!=NULL){
        if(info(P) == x){
            return P;
        }
        P = next(P);
    }
    return NULL;
}

void deleteFirst_Vaksin(List_vaksin &L, addr_vaksin &P){
    addr_vaksin Q = first(L);
    first(L) = next(first(L));
    prev(first(L)) = NULL;
    delete Q;
}

void deleteLast_Vaksin(List_vaksin &L, addr_vaksin &P){
    addr_vaksin Q = last(L);
    last(L) = prev(last(L));
    next(last(L)) = NULL;
    delete Q;
}

void deleteAfter_Vaksin(List_vaksin &L,addr_vaksin &P, addr_vaksin Q){
    addr_vaksin Z = first(L);
    while(Z !=NULL) {
        if(info(Z)==info(Q)){
            if(Z == first(L)){
            deleteFirst_Vaksin(L,P);
            }else if(next(Z) == NULL){
            deleteLast_Vaksin(L,P);
            }else if(Z != first(L) && next(Z) != NULL ){
            cout<<"Node Tengah"<<endl;
            }
        }Z = next(Z);
    }
}


void printVaksin(List_vaksin &L){
    addr_vaksin P = first(L);
    while(P != NULL){
        cout<<info(P)<<endl;
        P=next(P);
    }
}


void SearchInfoVaksin(List_vaksin L,addr_vaksin Q) {
    addr_vaksin P = first(L);
    while(P !=NULL) {
        if(info(P)==info(Q)){
        cout<<"- Vakasin "<<info(P)<<endl;
        }
        P = next(P);
    }
}
