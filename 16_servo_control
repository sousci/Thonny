import machine
import utime

def control_servos(current_angle_list, target_angle_list, transition_time, steps=100):
    # サーボモータ用のピン設定
    servo_pins = [machine.PWM(machine.Pin(i)) for i in range(16)]
    
    # PWMの周波数設定 (50Hz -> 20ms周期)
    for pin in servo_pins:
        pin.freq(50)

    # 徐々に変化させるためのステップ数
    step_time = transition_time / steps

    # ステップごとに角度を徐々に変化させる
    for step in range(steps):
        for i in range(16):
            current_angle = current_angle_list[i] + (target_angle_list[i] - current_angle_list[i]) * (step + 1) / steps
            pulse_width = 500 + (2000 - 500) * current_angle / 180
            duty_cycle = pulse_width / 20000 * 100
            servo_pins[i].duty_u16(int(duty_cycle * 65535 / 100))
        utime.sleep_ms(step_time)

# 角度の初期値を設定 (90度)
initial_angle_list = [90] * 16

# 初期値にサーボモータをセット
control_servos(initial_angle_list, initial_angle_list, 0)

# 動作例
target_angle_list = [0, 45, 90, 135, 180, 90, 45, 135, 180, 90, 135, 180, 90, 45, 135, 180]
transition_time = 2000  # ミリ秒
control_servos(initial_angle_list, target_angle_list, transition_time)
