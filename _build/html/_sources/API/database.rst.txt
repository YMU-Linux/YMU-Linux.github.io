=============
Database [DB]
=============


==========  =====================  =======================================================================  ==========================
Date        Competence / Topic     Learned Content, Procedure, Problems & Solutions                         Remarks
----------  ---------------------  -----------------------------------------------------------------------  --------------------------
2025-xx-xx  Relational Database    .. image:: img/rel_database.svg

                                   A relational database is structured as follows:

                                   1. **Tables:** Store entities (e.g., Customer, Order, Product). 
                                      Each table has:
                                      - **Rows (Records):** Individual entity instances.
                                      - **Columns (Fields):** Attributes describing the entity.

                                   2. **Primary Keys (PK):** Uniquely identify each row in a table.
                                      - Example: `customer_id` in the CUSTOMER table.

                                   3. **Foreign Keys (FK):** Connect tables by referencing primary keys in
                                       other tables.
                                      - Example: `customer_id` in ORDER table references CUSTOMER table.

                                   4. **Relationships:**
                                      - **One-to-Many (1:N):** One customer can place many orders.
                                      - **Many-to-Many (M:N):** Orders can include many products; products
                                      can appear in many orders.
                                        - Implemented via a junction table like `ORDER_PRODUCT`.
                                      - **One-to-One (1:1):** Rare; one row corresponds exactly to one row
                                      in another table.

                                   5. **Diagramming:** Use ER diagrams to visualize tables and relationshi
                                   ps.
                                      - Example:
                                        - CUSTOMER ||--o{ ORDER
                                        - ORDER ||--o{ ORDER_PRODUCT
                                        - PRODUCT ||--o{ ORDER_PRODUCT

==========  =====================  =======================================================================  ==========================

