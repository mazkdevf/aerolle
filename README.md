# aerolle
Joku koodin pätkä aerolle :D

```cpp
#include <iostream>
#include <chrono>
#include <ctime>
#include <thread>

class painikkeenpainaja {
private:
    int MikroservomoottoriPinni;
    int Aikavali;
    int PainikkeenTila;
public:
    painikkeenpainaja(int pin, int delay) : MikroservomoottoriPinni(pin), Aikavali(delay), PainikkeenTila(0) {}

    void aloita_looppi() {
        while (true) {
            std::time_t now = std::chrono::system_clock::to_time_t(std::chrono::system_clock::now());
            char buffer[26];
            ctime_s(buffer, sizeof(buffer), &now);
            std::this_thread::sleep_for(std::chrono::milliseconds(2000));
            std::cout << "[" << buffer << "] Käännytään oikealle\n\n" << std::endl;
            PainikkeenTila = 1;
            std::this_thread::sleep_for(std::chrono::milliseconds(2000));
            std::time_t now2 = std::chrono::system_clock::to_time_t(std::chrono::system_clock::now());
            ctime_s(buffer, sizeof(buffer), &now2);
            std::cout << "[" << buffer << "] Käännytään vasemmalle\n\n" << std::endl;
            PainikkeenTila = 0;

            std::this_thread::sleep_for(std::chrono::milliseconds(Aikavali));
        }
    }
};

int main() {
    int MikroservomoottoriPinni = 9;
    int Aikavali = 1 * 60 * 1000;

    painikkeenpainaja painikkeenpainaja_(MikroservomoottoriPinni, Aikavali);
    painikkeenpainaja_.aloita_looppi();

    return 0;
}
```
