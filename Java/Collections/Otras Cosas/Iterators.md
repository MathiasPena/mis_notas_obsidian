```java
List<String> lista = new ArrayList<>(Arrays.asList("A", "B", "C", "D"));
        
        // Uso de Iterator (para recorrer cualquier Collection)
        Iterator<String> iter = lista.iterator();
        while (iter.hasNext()) {
            String elemento = iter.next();
            if (elemento.equals("B")) {
                iter.remove(); // Eliminar elemento seguro
            }
        }
        
        // Uso de ListIterator (solo para List, permite recorrer en ambas direcciones)
        ListIterator<String> listIter = lista.listIterator();
        while (listIter.hasNext()) {
            System.out.println("Avanzando: " + listIter.next());
        }
        while (listIter.hasPrevious()) {
            System.out.println("Retrocediendo: " + listIter.previous());
        }
```
