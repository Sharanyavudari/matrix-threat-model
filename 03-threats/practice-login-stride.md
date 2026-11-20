| Flow | From → To | Rows to read | Letters to ask about |
|---|---|---|---|
| F1 | E1 User → P0 Web Server | 11, 7, 8 | S, T, R, I, D, E |
| F2 | P0 Web Server → P1 AuthN | 2, 6 | S, R, I, D, E |
| F3 | P1 AuthN → P2 Check Cred | 2, 6, 8 | S, T, R, I, D, E |
| F4 | P2 Check Cred → D1 User DB | 1, 9, 8 | S, T, R, I, D |
| F5 | D1 User DB → P2 Check Cred | 10, 5, 8 | S, T, R, I, D, E |
| F6 | P2 Check Cred → P1 AuthN | 2, 6, 8 | S, T, R, I, D, E |
| F7 | P1 AuthN → P0 Web Server | 2, 6 | S, R, I, D, E |
| F8 | P0 Web Server → E1 User | 3, 12, 8 | S, T, R, I, D |
