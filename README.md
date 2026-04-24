```mermaid
erDiagram
    FACT_EBAY_LISTINGS {
        string itemid
        string seller_name
        string location_country
        string item_condition
        string currency
        string shipping_cost_type
        string shipping_currency
        double price
        double shipping_cost
        boolean top_rated_buying_experience
        string search_category
        string buying_options
        date snapshot_dt
    }

    DIM_ITEMS {
        string itemid
        string title
        timestamp item_creation_ts
        string sub_sub_category_id
        date snapshot_dt
    }

    DIM_SELLERS {
        string seller_name
        double seller_feedback_percentage
        bigint seller_feedback_score
        date snapshot_dt
    }

    DIM_LOCATIONS {
        string location_country
        date snapshot_dt
    }

    DIM_CONDITIONS {
        string item_condition
        date snapshot_dt
    }

    DIM_CURRENCIES {
        string currency
        date snapshot_dt
    }

    DIM_LOGISTICS {
        string shipping_cost_type
        string shipping_currency
        bigint estimated_delivery_days
        date snapshot_dt
    }

    DIM_CAT {
        string category_id
        string category_name
        date snapshot_dt
    }

    DIM_SUB_CAT {
        string sub_category_id
        string sub_category_name
        string category_id
        date snapshot_dt
    }

    DIM_SUB_SUB_CAT {
        string sub_sub_category_id
        string sub_sub_category_name
        string sub_category_id
        date snapshot_dt
    }

    FACT_EBAY_LISTINGS }o--|| DIM_ITEMS : itemid
    FACT_EBAY_LISTINGS }o--|| DIM_SELLERS : seller_name
    FACT_EBAY_LISTINGS }o--|| DIM_LOCATIONS : location_country
    FACT_EBAY_LISTINGS }o--|| DIM_CONDITIONS : item_condition
    FACT_EBAY_LISTINGS }o--|| DIM_CURRENCIES : currency
    FACT_EBAY_LISTINGS }o--|| DIM_LOGISTICS : shipping_cost_type_shipping_currency

    DIM_ITEMS }o--|| DIM_SUB_SUB_CAT : sub_sub_category_id
    DIM_SUB_SUB_CAT }o--|| DIM_SUB_CAT : sub_category_id
    DIM_SUB_CAT }o--|| DIM_CAT : category_id
