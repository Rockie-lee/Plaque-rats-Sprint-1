erDiagram
    PLAYER {
        int player_id PK
        string username
        string email
        string password_hash
        datetime join_date
        datetime last_login
        int current_colony_id FK
    }

    COLONY {
        int colony_id PK
        int leader_id FK
        string colony_name
        int colony_size
        string location
        datetime created_at
        string status
    }

    PLAYER_STATS {
        int stat_id PK
        int player_id FK
        string stat_type
        int stat_value
        datetime timestamp
    }

    PLAGUE_RAT {
        int rat_id PK
        string species
        int health
        int strength
        int colony_id FK
        int evolution_stage
        string mutation_type
    }

    COLONY_RAT {
        int colony_id FK
        int rat_id FK
        string role
        datetime joined_at
    }

    GAME_EVENT {
        int event_id PK
        string event_type
        string description
        datetime timestamp
        int player_id FK
        int colony_id FK
    }

    COLONY_PROGRESS {
        int progress_id PK
        int colony_id FK
        string upgrade_type
        int upgrade_level
        datetime timestamp
    }

    ITEM {
        int item_id PK
        string item_name
        string item_type
    }

    ECONOMY {
        int transaction_id PK
        int player_id FK
        int item_id FK
        string transaction_type
        int amount
        datetime timestamp
    }

    PLAGUE {
        int plague_id PK
        string plague_name
        string description
        int effect_type_id FK
        int severity_id FK
        int duration
        int spread_rate
        datetime created_at
    }

    EFFECT_TYPE {
        int effect_type_id PK
        string effect_type_name
    }

    SEVERITY {
        int severity_id PK
        string severity_name
    }

    PLAGUE_RAT_RELATION {
        int relation_id PK
        int rat_id FK
        int plague_id FK
        datetime infection_date
        datetime recovery_date
    }

    PLAGUE_PLAYER_RELATION {
        int relation_id PK
        int player_id FK
        int plague_id FK
        datetime infection_date
        datetime recovery_date
    }

    WEATHER {
        int weather_id PK
        string weather_name
        int effect_id FK
    }

    WEATHER_EFFECTS {
        int effect_id PK
        string effect_name
        string effect_description
    }

    DAY_NIGHT_TIME {
        int time_id PK
        string day_night_period
        time start_time
        time end_time
        string effect
    }

    BATTLE {
        int battle_id PK
        string battle_type
        int winner_colony_id FK
        datetime battle_date
    }

    BATTLE_PARTICIPANT {
        int participant_id PK
        int battle_id FK
        int colony_id FK
        int num_units
    }

    ACHIEVEMENT {
        int achievement_id PK
        string achievement_name
        string achievement_description
    }

    PLAYER_ACHIEVEMENT {
        int player_achievement_id PK
        int player_id FK
        int achievement_id FK
        datetime earned_at
    }

    %% Relationships
    PLAYER ||--o{ COLONY : "owns"
    PLAYER ||--o{ PLAYER_STATS : "has stats"
    COLONY ||--o{ COLONY_RAT : "has"
    PLAGUE_RAT ||--o{ COLONY_RAT : "belongs to"
    COLONY ||--o{ GAME_EVENT : "affected by"
    PLAYER ||--o{ GAME_EVENT : "caused by"
    COLONY ||--o{ COLONY_PROGRESS : "upgrades"
    PLAYER ||--o{ ECONOMY : "transacts"
    ITEM ||--o{ ECONOMY : "involves"
    PLAGUE ||--o{ PLAGUE_RAT_RELATION : "infects"
    PLAGUE_RAT ||--o{ PLAGUE_RAT_RELATION : "is infected"
    PLAGUE ||--o{ PLAGUE_PLAYER_RELATION : "infects"
    PLAYER ||--o{ PLAGUE_PLAYER_RELATION : "can be infected"
    PLAGUE ||--o{ EFFECT_TYPE : "causes"
    PLAGUE ||--o{ SEVERITY : "has severity"
    WEATHER_EFFECTS ||--o{ WEATHER : "affects"
    WEATHER ||--o{ GAME_EVENT : "affects"
    DAY_NIGHT_TIME ||--o{ GAME_EVENT : "influences"
    BATTLE ||--o{ BATTLE_PARTICIPANT : "includes"
    COLONY ||--o{ BATTLE_PARTICIPANT : "participates in"
    PLAYER ||--o{ PLAYER_ACHIEVEMENT : "earns"
    ACHIEVEMENT ||--o{ PLAYER_ACHIEVEMENT : "is awarded"
